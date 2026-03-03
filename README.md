# Cortex Code Project Planner Skill

A reusable **Cortex Code skill** that generates complete project implementation plans from any requirements markdown file. It estimates Cortex Code time, human effort, token usage, Snowflake credits, and **human-only development time** for each task -- so you can see exactly how much time Cortex Code saves compared to fully manual development.

## What It Does

Given any markdown requirements document, the skill will:

1. **Parse** the requirements and identify objectives, constraints, and components
2. **Decompose** into typed, complexity-rated work items (SQL DDL, Python modules, Streamlit apps, dbt models, etc.)
3. **Estimate** five metrics per task: CoCo time, human effort (with CoCo), tokens, Snowflake credits, and human-only development time
4. **Compare** CoCo-assisted development vs. fully human development with time saved and speedup ratios
5. **Generate** a phased implementation plan with dependency graph, subtotals, overhead multipliers, human-only comparison, and recommendations

## Key Features

- **Rapid development cycle estimates** -- CoCo times reflect parallel tool execution, autonomous iteration, single-shot generation, and built-in verification loops
- **Lightweight human effort** -- human involvement is scoped to quick review, spot-check testing, domain input, deployment approval, and course correction
- **Human-only comparison** -- every plan includes a "What if this was built entirely by humans?" section with per-phase breakdown, time saved, and speedup factor
- **Separate overhead multipliers** -- CoCo+Human and Human-Only each have their own realistic overhead factors

## Installation

### Option 1: Import from GitHub (Remote Skill)

Add this to `~/.snowflake/cortex/skills.json` (create the file if it doesn't exist):

```json
{
  "remote": [
    {
      "source": "https://github.com/curious-bigcat/coco-project-plan",
      "ref": "main",
      "skills": [{ "name": "project-planner" }]
    }
  ]
}
```

### Option 2: Install Locally (Global Skill)

```bash
git clone https://github.com/curious-bigcat/coco-project-plan.git
cp -r coco-project-plan/skills/project-planner ~/.snowflake/cortex/skills/
```

### Option 3: Project-Level Skill

Copy into any project's `.cortex/skills/` directory:

```bash
cp -r skills/project-planner <your-project>/.cortex/skills/
```

The skill will be available whenever Cortex Code runs in that project directory.

## Usage

Invoke the skill by passing any requirements markdown file:

```
$project-planner @path/to/your/requirements.md
```

The requirements file can describe any project -- a data pipeline, a Streamlit app, a Cortex Agent, a dbt project, an API integration, etc. The skill adapts its task categories and estimates to match.

### Trigger Keywords

The skill also activates on natural language requests containing:
- "project plan", "estimate project", "plan implementation"
- "effort estimate", "token estimate", "credit estimate", "cost estimate"
- "requirements analysis", "project breakdown", "implementation plan"
- "how long will it take"

## Example Output

The skill produces a structured plan with per-task estimates and a human-only comparison:

```
| # | Task                  | Type              | Complexity | CoCo Time  | Human Effort | Tokens (K) | Credits   | Human-Only Time |
|---|-----------------------|-------------------|-----------|------------|-------------|-----------|-----------|-----------------|
| 1 | Create database       | SQL Table / View  | S         | 1-3 min    | 2-5 min     | 5-15K     | 0.01-0.05 | 15-30 min       |
| 2 | Build ETL pipeline    | ETL Pipeline/DAG  | C         | 30-55 min  | 30-60 min   | 100-200K  | 0.35-0.70 | 4-8 hr          |
```

Including phase subtotals, dependency graphs, overhead multipliers, and a human-only comparison section:

```
| Metric                | With Cortex Code   | Human-Only         |
|-----------------------|--------------------|--------------------|
| Total Development Time| 2-4 hr             | 12-24 hr           |
| Time Saved            | —                  | 10-20 hr           |
| Speedup Factor        | —                  | 4x - 6x faster     |
```

## Skill File Structure

```
skills/project-planner/
├── SKILL.md                              # Main skill instructions and workflow
└── references/
    ├── estimation-heuristics.md          # Lookup tables for all metrics by task type, complexity, and human-only comparison
    └── plan-template.md                  # Output format template
```
## License

MIT
