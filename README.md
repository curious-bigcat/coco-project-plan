# Cortex Code Project Planner Skill

A reusable **Cortex Code skill** that generates complete project implementation plans from any requirements markdown file. It estimates Cortex Code time, human effort, token usage, and Snowflake credits for each task.

## What It Does

Given any markdown requirements document, the skill will:

1. **Parse** the requirements and identify objectives, constraints, and components
2. **Decompose** into typed, complexity-rated work items (SQL DDL, Python modules, Streamlit apps, dbt models, etc.)
3. **Estimate** four metrics per task: CoCo time, human effort, tokens, and Snowflake credits
4. **Generate** a phased implementation plan with dependency graph, subtotals, overhead multipliers, and recommendations

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

The skill produces a structured plan with per-task estimates:

```
| # | Task                  | Type              | Complexity | CoCo Time  | Human Effort | Tokens (K) | Credits   |
|---|-----------------------|-------------------|-----------|------------|-------------|-----------|-----------|
| 1 | Create database       | SQL Table / View  | S         | 2-5 min    | 5-10 min    | 5-15K     | 0.01-0.05 |
| 2 | Build ETL pipeline    | ETL Pipeline/DAG  | C         | 40-75 min  | 60-120 min  | 100-200K  | 0.35-0.70 |
```

Including phase subtotals, dependency graphs, overhead multipliers, and a final adjusted estimate.

## Skill File Structure

```
skills/project-planner/
├── SKILL.md                              # Main skill instructions and workflow
└── references/
    ├── estimation-heuristics.md          # Lookup tables for all 4 metrics by task type and complexity
    └── plan-template.md                  # Output format template
```

## Supported Task Types

The skill recognizes and estimates these task categories:

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

## License

MIT
