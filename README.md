# CoVe Snowflake - Chain of Verification with Snowflake Cortex

A **Chain of Verification (CoVe)** system that reduces LLM hallucination using Snowflake Cortex AI services. Includes a complete project definition, implementation plan, and a reusable **Cortex Code skill** for project planning.

## What's Included

| File | Description |
|------|-------------|
| `PROJECT_DEFINITION.md` | Full architecture, schema design, and implementation spec for the CoVe system |
| `project-plan.md` | Generated implementation plan with time, effort, token, and credit estimates |
| `skills/project-planner/SKILL.md` | Cortex Code skill for generating project plans from requirements docs |
| `skills/project-planner/references/` | Estimation heuristics and plan output template used by the skill |

## Using the Project Planner as a Cortex Code Skill

The `project-planner` skill can be imported into any Cortex Code session to generate implementation plans from requirements documents. It estimates Cortex Code time, human effort, token usage, and Snowflake credits for each task.

### Option 1: Import from GitHub (Remote Skill)

Add this to your `~/.snowflake/cortex/skills.json` (create the file if it doesn't exist):

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

Then in any Cortex Code session:

```
$project-planner @path/to/your/requirements.md
```

### Option 2: Install Locally (Global Skill)

Clone and copy the skill into your global skills directory:

```bash
git clone https://github.com/curious-bigcat/coco-project-plan.git
cp -r coco-project-plan/skills/project-planner ~/.snowflake/cortex/skills/
```

Then use it in Cortex Code:

```
$project-planner @path/to/your/requirements.md
```

### Option 3: Project-Level Skill

Copy the skill into any project's `.cortex/skills/` directory:

```bash
cp -r skills/project-planner <your-project>/.cortex/skills/
```

The skill will be available whenever Cortex Code runs in that project directory.

## Skill Usage

Once installed, invoke the skill by passing a requirements markdown file:

```
$project-planner @requirements.md
```

The skill will:

1. **Parse** the requirements document
2. **Decompose** into typed, complexity-rated work items
3. **Estimate** CoCo time, human effort, tokens, and Snowflake credits per task
4. **Generate** a phased implementation plan with dependency graph and totals

### Example Output

The skill produces a structured plan with per-task estimates:

```
| # | Task                  | Type              | Complexity | CoCo Time  | Human Effort | Tokens (K) | Credits   |
|---|-----------------------|-------------------|-----------|------------|-------------|-----------|-----------|
| 1 | Create database       | SQL Table / View  | S         | 2-5 min    | 5-10 min    | 5-15K     | 0.01-0.05 |
| 2 | Build ETL pipeline    | ETL Pipeline/DAG  | C         | 40-75 min  | 60-120 min  | 100-200K  | 0.35-0.70 |
```

## Skill File Structure

```
skills/project-planner/
├── SKILL.md                              # Main skill instructions
└── references/
    ├── estimation-heuristics.md          # Lookup tables for all 4 metrics
    └── plan-template.md                  # Output format template
```

## About the CoVe Project

The CoVe system implements a 4-step verification workflow:

1. **Baseline Response** -- Generate initial LLM answer via Cortex Complete
2. **Plan Verification** -- Extract fact claims and generate verification questions
3. **Execute Verification** -- Verify claims using Cortex Analyst (structured data) and Cortex Search (knowledge base)
4. **Final Response** -- Produce a corrected response with verified facts

See `PROJECT_DEFINITION.md` for full architecture details.

## License

MIT
