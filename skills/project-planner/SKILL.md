---
name: project-planner
description: "Generate a complete project implementation plan with Cortex Code time, human effort, token usage, and Snowflake credit estimates from a requirements document. Produces the full plan end-to-end in one shot. Use when: user provides a business or technical requirements markdown file and wants a plan, estimation, cost projection, or project breakdown. Triggers: project plan, estimate project, plan implementation, effort estimate, token estimate, credit estimate, cost estimate, requirements analysis, project breakdown, implementation plan, how long will it take, plan mode estimate."
---

# Project Planner

Generate a complete, end-to-end project implementation plan with per-task estimates for:
1. **Cortex Code implementation time** -- how long CoCo takes to build each task
2. **Human effort required** -- review, testing, deployment, domain expertise
3. **Token usage** -- input + output tokens consumed across iterations
4. **Snowflake credits** -- SQL execution, Cortex AI calls, warehouse compute during development

**CRITICAL:** Do NOT stop after the work breakdown. Run all steps end-to-end and produce the complete plan with all estimates in a single output.

## Setup

1. **Load** `references/estimation-heuristics.md` -- required for all estimations
2. **Load** `references/plan-template.md` -- required for output formatting

## Workflow

### Step 1: Ingest Requirements

**Goal:** Read and understand the user's requirements document.

**Actions:**

1. **Ask** user for their requirements file if not already provided:
   ```
   Please provide the path to your requirements document (markdown file).
   You can also paste the requirements directly or use @filename.
   ```

2. **Read** the requirements file completely.

3. **Identify** and list:
   - Project name / title
   - High-level objectives (what is being built)
   - Functional requirements (features, behaviors, business rules)
   - Non-functional requirements (performance, security, compliance)
   - Technical constraints (specific technologies, Snowflake features, integrations)
   - Data sources and targets
   - User-facing components (dashboards, apps, APIs)

**Output:** Parsed requirements understanding (internal -- do not present separately)

**Next:** Immediately proceed to Step 2 (do NOT stop here)

---

### Step 2: Categorize Work Items

**Goal:** Break requirements into concrete, typed, and complexity-rated work items.

**Actions:**

1. **Decompose** each requirement into individual implementation tasks.

2. **Classify** each task by type (use these categories):
   - SQL Table / View DDL
   - Stored Procedure / UDF
   - dbt Model (SQL or Python)
   - dbt Tests + Schema YAML
   - Streamlit App / Page
   - Python Script / Module
   - ETL Pipeline / DAG
   - Cortex Agent Definition
   - Semantic View / Model
   - API Endpoint / Integration
   - Dynamic Table
   - Task / Schedule
   - Config / YAML / Manifest
   - Documentation (only if explicitly requested)

3. **Rate complexity** for each task (Simple / Medium / Complex / Very Complex):
   - Simple: Single file, clear spec, no dependencies, < 100 lines
   - Medium: 1-3 files, some logic, minor dependencies, 100-300 lines
   - Complex: 3-5 files, business logic, multiple dependencies, 300-600 lines
   - Very Complex: 5+ files, intricate logic, cross-system dependencies, 600+ lines

4. **Identify dependencies** between tasks.

5. **Group tasks into phases** (typically 3-5 phases):
   - Phase 1: Foundation (schemas, tables, base config)
   - Phase 2: Core Logic (models, procedures, pipelines)
   - Phase 3: Integration (connecting components, APIs)
   - Phase 4: Presentation (Streamlit, dashboards, agents)
   - Phase 5: Testing & Polish (tests, docs, deployment config)

   Adjust phases to match the project. Not all phases apply to every project.

**Output:** Categorized work breakdown (used in next step -- do NOT present separately)

**Next:** Immediately proceed to Step 3 (do NOT stop here)

---

### Step 3: Estimate Per Task

**Goal:** Calculate all 4 estimates for every task using the heuristics tables.

**Actions:**

1. **For each task**, look up estimates from `references/estimation-heuristics.md`:
   - **Cortex Code time** (min-max minutes)
   - **Human effort** (min-max minutes)
   - **Token usage** (min-max in thousands)
   - **Snowflake credits** (min-max)

2. **Calculate phase subtotals** by summing min and max for each metric.

3. **Calculate raw project totals** by summing all phase subtotals.

4. **Apply overhead multipliers** based on project characteristics:
   - If requirements are vague or incomplete: apply 1.20-1.40x rework multiplier to all
   - If project spans multiple sessions: apply 1.10-1.20x token multiplier for context switching
   - If patterns are new to the team: apply 1.15-1.30x to human effort and CoCo time
   - Add flat amounts for production deployment (+15-30 min), CI/CD (+10-20 min) if applicable

5. **Compute adjusted totals** = raw totals * applicable multipliers.

6. **Convert large minute values** to hours where > 120 min (e.g., "150 min (2.5h)").

**Output:** Complete estimation data (used in next step)

**Next:** Immediately proceed to Step 4 (do NOT stop here)

---

### Step 4: Generate Complete Plan Document

**Goal:** Produce the final plan using `references/plan-template.md` and present it.

**Actions:**

1. **Fill in the template** with all data from Steps 1-3:
   - Project name, date, source file
   - Executive summary with adjusted total estimate ranges
   - Per-phase task tables with ALL 4 METRICS per task row:
     - `| # | Task | Type | Complexity | CoCo Time | Human Effort | Tokens (K) | Credits |`
   - Phase subtotals
   - Dependency graph (ASCII art)
   - Raw vs adjusted totals with overhead explanation
   - Assumptions and risks
   - Recommendations

2. **Present** the complete plan to the user in a single output.

3. **After the plan**, offer next steps:
   ```
   Would you like me to:
   1. Adjust any estimates or task classifications?
   2. Save this plan to a file?
   3. Start implementing Phase 1?
   ```

**If user wants to save:** Write to a markdown file at user-specified location (default: `./project-plan.md`).
**If user wants to implement:** Begin with Phase 1, Task 1 using Cortex Code's normal workflow.
**If user wants adjustments:** Modify and re-present.

**Output:** Final plan document with all estimates

---

## Stopping Points

- **Before Step 1:** Only if requirements are not provided -- ask user for the file
- **After Step 4:** Present final plan and wait for user's choice (adjust / save / implement)
- Do NOT stop between Steps 1-4. Produce the complete plan end-to-end.

**Resume rule:** On user approval of final plan, proceed with their chosen action.

## Error Handling

**If requirements file is not found:**
- Ask user to verify the path or paste content directly

**If requirements are too vague to decompose:**
- List what is unclear
- Ask user to clarify specific sections before proceeding
- Do NOT guess at missing requirements

**If a task type doesn't match any heuristic category:**
- Use the closest matching category
- Note the approximation in the Assumptions section

**If the project is very large (>50 tasks):**
- Still produce the full plan, but note in Recommendations that implementation should be split into sub-projects

## Output

A complete project implementation plan in markdown containing:
- Phased task breakdown with dependencies
- Per-task estimates for ALL 4 metrics: CoCo time, human effort, tokens, credits
- Phase subtotals for all metrics
- Raw and adjusted totals with overhead multipliers explained
- Dependency graph
- Assumptions, risks, and recommendations
- Disclaimer about estimate accuracy
