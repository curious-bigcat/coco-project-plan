# Estimation Heuristics

Use these tables to estimate effort, tokens, and credits for each work item.
All estimates are **ranges (min-max)**. Actual values depend on requirements clarity, iteration cycles, and codebase complexity.

## Disclaimer

Present this disclaimer in every plan output:
> Estimates are approximations based on typical Cortex Code usage patterns. Actual values vary based on requirement complexity, iteration count, existing codebase size, and user interaction patterns. Token estimates include context reads, generation, and expected iterations. Credit estimates cover development-time compute only, not production workloads.

---

## Complexity Classification

Classify each work item before estimating:

| Complexity | Criteria |
|-----------|---------|
| **Simple** | Single file, clear spec, no dependencies, < 100 lines of code |
| **Medium** | 1-3 files, some logic, minor dependencies, 100-300 lines |
| **Complex** | 3-5 files, business logic, multiple dependencies, 300-600 lines |
| **Very Complex** | 5+ files, intricate logic, cross-system dependencies, 600+ lines |

---

## Cortex Code Implementation Time Estimates

Time CoCo spends actively generating, iterating, and validating.

| Task Type | Simple | Medium | Complex | Very Complex |
|-----------|--------|--------|---------|--------------|
| SQL Table / View DDL | 2-5 min | 5-10 min | 10-20 min | 20-40 min |
| Stored Procedure / UDF | 5-10 min | 10-20 min | 20-40 min | 40-75 min |
| dbt Model (SQL) | 3-8 min | 8-15 min | 15-30 min | 30-60 min |
| dbt Model (Python) | 5-10 min | 10-20 min | 20-40 min | 40-75 min |
| dbt Tests + Schema YAML | 2-5 min | 5-10 min | 10-20 min | 20-35 min |
| Streamlit App / Page | 10-20 min | 20-40 min | 40-75 min | 75-120 min |
| Python Script / Module | 5-10 min | 10-25 min | 25-50 min | 50-90 min |
| ETL Pipeline / DAG | 10-20 min | 20-40 min | 40-75 min | 75-120 min |
| Cortex Agent Definition | 8-15 min | 15-30 min | 30-50 min | 50-90 min |
| Semantic View / Model | 5-10 min | 10-20 min | 20-40 min | 40-70 min |
| API Endpoint / Integration | 5-15 min | 15-30 min | 30-55 min | 55-90 min |
| Dynamic Table | 3-8 min | 8-15 min | 15-30 min | 30-50 min |
| Task / Schedule | 3-5 min | 5-10 min | 10-20 min | 20-35 min |
| Config / YAML / Manifest | 2-5 min | 5-10 min | 10-15 min | 15-25 min |
| Documentation (if requested) | 3-8 min | 8-15 min | 15-25 min | 25-40 min |

---

## Human Effort Estimates

Time humans spend on review, testing, domain input, deployment, and course correction.

| Task Type | Simple | Medium | Complex | Very Complex |
|-----------|--------|--------|---------|--------------|
| SQL Table / View DDL | 5-10 min | 10-20 min | 20-40 min | 40-60 min |
| Stored Procedure / UDF | 10-20 min | 20-40 min | 40-75 min | 75-120 min |
| dbt Model (SQL) | 10-15 min | 15-30 min | 30-50 min | 50-90 min |
| dbt Model (Python) | 10-20 min | 20-40 min | 40-60 min | 60-100 min |
| dbt Tests + Schema YAML | 5-10 min | 10-20 min | 20-35 min | 35-60 min |
| Streamlit App / Page | 15-30 min | 30-60 min | 60-120 min | 120-180 min |
| Python Script / Module | 10-20 min | 20-40 min | 40-75 min | 75-120 min |
| ETL Pipeline / DAG | 15-30 min | 30-60 min | 60-120 min | 120-180 min |
| Cortex Agent Definition | 15-25 min | 25-45 min | 45-75 min | 75-120 min |
| Semantic View / Model | 10-20 min | 20-40 min | 40-60 min | 60-100 min |
| API Endpoint / Integration | 10-25 min | 25-50 min | 50-90 min | 90-150 min |
| Dynamic Table | 5-15 min | 15-30 min | 30-50 min | 50-80 min |
| Task / Schedule | 5-10 min | 10-20 min | 20-35 min | 35-60 min |
| Config / YAML / Manifest | 5-10 min | 10-15 min | 15-25 min | 25-40 min |
| Documentation (if requested) | 5-10 min | 10-20 min | 20-35 min | 35-60 min |

**Human effort includes:** code review, manual testing, UAT, domain clarification, deployment steps, security review, and iteration feedback.

---

## Token Usage Estimates

Estimated input + output tokens per task (in thousands). Includes context reads, generation, and ~1-3 iterations.

| Task Type | Simple | Medium | Complex | Very Complex |
|-----------|--------|--------|---------|--------------|
| SQL Table / View DDL | 5-15K | 15-35K | 35-70K | 70-120K |
| Stored Procedure / UDF | 10-30K | 30-60K | 60-120K | 120-200K |
| dbt Model (SQL) | 8-20K | 20-45K | 45-90K | 90-150K |
| dbt Model (Python) | 10-30K | 30-60K | 60-110K | 110-180K |
| dbt Tests + Schema YAML | 5-15K | 15-30K | 30-60K | 60-100K |
| Streamlit App / Page | 20-50K | 50-100K | 100-200K | 200-350K |
| Python Script / Module | 15-35K | 35-70K | 70-150K | 150-250K |
| ETL Pipeline / DAG | 20-50K | 50-100K | 100-200K | 200-350K |
| Cortex Agent Definition | 15-40K | 40-80K | 80-150K | 150-250K |
| Semantic View / Model | 10-30K | 30-60K | 60-120K | 120-200K |
| API Endpoint / Integration | 15-40K | 40-80K | 80-160K | 160-270K |
| Dynamic Table | 8-20K | 20-40K | 40-80K | 80-140K |
| Task / Schedule | 5-12K | 12-25K | 25-50K | 50-90K |
| Config / YAML / Manifest | 3-10K | 10-20K | 20-40K | 40-70K |

**Token formula reference:** ~1.3 tokens per character of code. Each file read ~2-5K tokens. Each generation cycle ~5-20K tokens. Expect 1-3 iterations per task.

---

## Snowflake Credit Estimates

Credits consumed during development (SQL execution, Cortex AI calls, warehouse compute on XS).

| Task Type | Simple | Medium | Complex | Very Complex |
|-----------|--------|--------|---------|--------------|
| SQL Table / View DDL | 0.01-0.05 | 0.05-0.15 | 0.15-0.30 | 0.30-0.50 |
| Stored Procedure / UDF | 0.02-0.10 | 0.10-0.25 | 0.25-0.50 | 0.50-0.80 |
| dbt Model (SQL) | 0.02-0.08 | 0.08-0.20 | 0.20-0.40 | 0.40-0.70 |
| dbt Model (Python) | 0.03-0.10 | 0.10-0.25 | 0.25-0.50 | 0.50-0.80 |
| dbt Tests + Schema YAML | 0.02-0.08 | 0.08-0.15 | 0.15-0.30 | 0.30-0.50 |
| Streamlit App / Page | 0.05-0.15 | 0.15-0.35 | 0.35-0.60 | 0.60-1.00 |
| Python Script / Module | 0.02-0.08 | 0.08-0.20 | 0.20-0.40 | 0.40-0.70 |
| ETL Pipeline / DAG | 0.05-0.15 | 0.15-0.35 | 0.35-0.70 | 0.70-1.20 |
| Cortex Agent Definition | 0.05-0.20 | 0.20-0.50 | 0.50-0.80 | 0.80-1.50 |
| Semantic View / Model | 0.03-0.10 | 0.10-0.25 | 0.25-0.50 | 0.50-0.80 |
| API Endpoint / Integration | 0.03-0.12 | 0.12-0.30 | 0.30-0.55 | 0.55-0.90 |
| Dynamic Table | 0.02-0.08 | 0.08-0.20 | 0.20-0.40 | 0.40-0.65 |
| Task / Schedule | 0.01-0.05 | 0.05-0.12 | 0.12-0.25 | 0.25-0.45 |
| Config / YAML / Manifest | 0.01-0.03 | 0.03-0.08 | 0.08-0.15 | 0.15-0.25 |

**Credit assumptions:**
- XS warehouse: ~0.0003 credits/second active
- Each SQL execution: ~0.005-0.02 credits
- Each Cortex AI function call: ~0.01-0.05 credits
- dbt build (per model): ~0.01-0.05 credits
- Streamlit local dev session: ~0.05-0.15 credits

---

## Overhead Multipliers

Apply these to raw totals for a more realistic project estimate:

| Factor | Multiplier | Applies To |
|--------|-----------|------------|
| Integration testing (cross-component) | 1.15-1.25x | Human effort |
| Context switching (multi-session) | 1.10-1.20x | Tokens |
| Rework from unclear requirements | 1.20-1.40x | All estimates |
| First-time patterns (new to team) | 1.15-1.30x | Human effort, CoCo time |
| Production deployment & monitoring setup | +15-30 min flat | Human effort |
| CI/CD pipeline setup | +10-20 min flat | Human effort |
