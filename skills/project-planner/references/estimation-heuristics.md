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

Time CoCo spends actively generating, iterating, and validating. These reflect Cortex Code's rapid development cycle -- parallel tool execution, autonomous iteration, and single-shot generation for well-specified tasks.

| Task Type | Simple | Medium | Complex | Very Complex |
|-----------|--------|--------|---------|--------------|
| SQL Table / View DDL | 1-3 min | 3-7 min | 7-15 min | 15-30 min |
| Stored Procedure / UDF | 3-7 min | 7-15 min | 15-30 min | 30-55 min |
| dbt Model (SQL) | 2-5 min | 5-12 min | 12-25 min | 25-45 min |
| dbt Model (Python) | 3-7 min | 7-15 min | 15-30 min | 30-55 min |
| dbt Tests + Schema YAML | 1-3 min | 3-7 min | 7-15 min | 15-25 min |
| Streamlit App / Page | 7-15 min | 15-30 min | 30-55 min | 55-90 min |
| Python Script / Module | 3-7 min | 7-18 min | 18-35 min | 35-65 min |
| ETL Pipeline / DAG | 7-15 min | 15-30 min | 30-55 min | 55-90 min |
| Cortex Agent Definition | 5-10 min | 10-22 min | 22-40 min | 40-65 min |
| Semantic View / Model | 3-7 min | 7-15 min | 15-30 min | 30-50 min |
| API Endpoint / Integration | 3-10 min | 10-22 min | 22-40 min | 40-65 min |
| Dynamic Table | 2-5 min | 5-12 min | 12-22 min | 22-38 min |
| Task / Schedule | 2-4 min | 4-8 min | 8-15 min | 15-25 min |
| Config / YAML / Manifest | 1-3 min | 3-7 min | 7-12 min | 12-20 min |
| Documentation (if requested) | 2-5 min | 5-10 min | 10-18 min | 18-30 min |

**CoCo rapid-cycle factors:** Single-shot generation for simple tasks, parallel file reads and writes, autonomous error correction without human round-trips, and built-in verification loops reduce elapsed time by ~25-35% compared to traditional AI-assisted development.

---

## Human Effort Estimates (with Cortex Code)

Time humans spend alongside CoCo on quick review, spot-check testing, domain input, deployment approval, and course correction. Because CoCo handles implementation, iteration, and self-correction autonomously, human involvement is focused and lightweight.

| Task Type | Simple | Medium | Complex | Very Complex |
|-----------|--------|--------|---------|--------------|
| SQL Table / View DDL | 2-5 min | 5-10 min | 10-20 min | 20-35 min |
| Stored Procedure / UDF | 5-10 min | 10-20 min | 20-40 min | 40-65 min |
| dbt Model (SQL) | 5-10 min | 10-18 min | 18-30 min | 30-50 min |
| dbt Model (Python) | 5-10 min | 10-20 min | 20-35 min | 35-55 min |
| dbt Tests + Schema YAML | 3-5 min | 5-10 min | 10-20 min | 20-35 min |
| Streamlit App / Page | 8-15 min | 15-30 min | 30-60 min | 60-100 min |
| Python Script / Module | 5-10 min | 10-20 min | 20-40 min | 40-65 min |
| ETL Pipeline / DAG | 8-15 min | 15-30 min | 30-60 min | 60-100 min |
| Cortex Agent Definition | 8-15 min | 15-25 min | 25-45 min | 45-70 min |
| Semantic View / Model | 5-10 min | 10-20 min | 20-35 min | 35-55 min |
| API Endpoint / Integration | 5-12 min | 12-25 min | 25-50 min | 50-80 min |
| Dynamic Table | 3-8 min | 8-15 min | 15-30 min | 30-45 min |
| Task / Schedule | 3-5 min | 5-10 min | 10-20 min | 20-35 min |
| Config / YAML / Manifest | 2-5 min | 5-8 min | 8-15 min | 15-25 min |
| Documentation (if requested) | 3-5 min | 5-10 min | 10-20 min | 20-35 min |

**Human effort breakdown:**
- **Review** (~30%): Quick scan of CoCo-generated code, approve or request changes
- **Testing** (~25%): Spot-check outputs, run UAT scenarios, validate edge cases
- **Domain input** (~20%): Provide business rules, clarify requirements, answer CoCo's questions
- **Deployment** (~15%): Approve PRs, trigger deployments, verify production behavior
- **Course correction** (~10%): Redirect CoCo when output drifts, adjust priorities mid-flight

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

## Human-Only Development Estimates (No Cortex Code)

Estimated time for **human developers working without Cortex Code** to complete the same tasks. Use these to produce a "What if this project was built entirely by humans?" comparison. Estimates assume a competent developer familiar with Snowflake and the relevant tooling, working in a standard development environment with typical review/test/deploy cycles.

| Task Type | Simple | Medium | Complex | Very Complex |
|-----------|--------|--------|---------|--------------|
| SQL Table / View DDL | 15-30 min | 30-60 min | 1-2 hr | 2-4 hr |
| Stored Procedure / UDF | 30-60 min | 1-2 hr | 2-4 hr | 4-8 hr |
| dbt Model (SQL) | 20-45 min | 45-90 min | 1.5-3 hr | 3-6 hr |
| dbt Model (Python) | 30-60 min | 1-2 hr | 2-4 hr | 4-8 hr |
| dbt Tests + Schema YAML | 15-30 min | 30-60 min | 1-2 hr | 2-4 hr |
| Streamlit App / Page | 1-2 hr | 2-4 hr | 4-8 hr | 8-16 hr |
| Python Script / Module | 30-60 min | 1-2 hr | 2-5 hr | 5-10 hr |
| ETL Pipeline / DAG | 1-2 hr | 2-4 hr | 4-8 hr | 8-16 hr |
| Cortex Agent Definition | 45-90 min | 1.5-3 hr | 3-6 hr | 6-12 hr |
| Semantic View / Model | 30-60 min | 1-2 hr | 2-4 hr | 4-8 hr |
| API Endpoint / Integration | 30-90 min | 1.5-3 hr | 3-6 hr | 6-12 hr |
| Dynamic Table | 20-45 min | 45-90 min | 1.5-3 hr | 3-5 hr |
| Task / Schedule | 15-30 min | 30-60 min | 1-2 hr | 2-4 hr |
| Config / YAML / Manifest | 10-20 min | 20-45 min | 45-90 min | 1.5-3 hr |
| Documentation (if requested) | 15-30 min | 30-60 min | 1-2 hr | 2-4 hr |

**Human-only estimates include:** requirements analysis, design/research, implementation, self-review, testing, debugging, code review with peers, deployment, and documentation. These represent end-to-end developer time, not just coding.

**Human-only overhead multipliers** (apply on top of raw human-only totals):

| Factor | Multiplier | Rationale |
|--------|-----------|-----------|
| Team coordination & meetings | 1.20-1.40x | Standups, design discussions, PR reviews, context sharing |
| Context switching & interruptions | 1.15-1.30x | Multitasking across projects, Slack/email, meeting breaks |
| Ramp-up on unfamiliar tools/patterns | 1.20-1.50x | Learning Snowflake features, reading docs, trial-and-error |
| Environment setup & tooling issues | +1-4 hr flat | Local env, dependencies, access provisioning, CI/CD config |
| QA / staging validation | 1.10-1.25x | Manual test runs, environment promotion, regression checks |

---

## Overhead Multipliers (Cortex Code + Human)

Apply these to raw CoCo+Human totals for a more realistic project estimate. These are tuned for the rapid development cycle where CoCo drives implementation and humans focus on review and steering.

| Factor | Multiplier | Applies To |
|--------|-----------|------------|
| Integration testing (cross-component) | 1.10-1.20x | Human effort |
| Context switching (multi-session) | 1.10-1.20x | Tokens |
| Rework from unclear requirements | 1.15-1.30x | All estimates |
| First-time patterns (new to team) | 1.10-1.20x | Human effort, CoCo time |
| Production deployment & monitoring setup | +10-20 min flat | Human effort |
| CI/CD pipeline setup | +5-15 min flat | Human effort |
