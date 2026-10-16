# Signed AI Exposure (S / C / I) and Workflow Completeness (C*): scores for every task and occupation in the US economy

This repository carries **two measures built from one grading** of the 17,536 O*NET task statements (798 SOC occupations), scored under six large language models from four developers.

**1. The signed measure.** Each occupation's task mass split into a **substitution** margin S (AI performs the task alone), a **complement** margin C = m2 + m3 (AI assists; a human delivers in real time, or signs off), and an **inert** margin I (physical work AI cannot perform). The sign is the point: S predicts negative employment effects, C positive ones, and a single unsigned index cannot see either.

**2. The unsigned ceiling, C\*.** Workflow Completeness, C* = S + (2/3)m3 + (1/3)m2: the one-number summary for uses where a scalar suffices (adoption and productivity applications), included for comparability with the exposure-index literature.

**Main rater: Claude Sonnet 4 (the papers' incumbent).** Scores under all six raters are included so the stability of any result can be checked directly.

## Files

**`data/occupations.csv`**: one row per 6-digit SOC occupation (n = 798). The file most users want: merge on `soc6` and go.

| column | meaning |
|---|---|
| `soc6` | 6-digit SOC code (e.g. 11-1011) |
| `title` | O*NET occupation title |
| `S` | substitution margin: importance-weighted share of tasks AI performs alone (score 4) |
| `m2` | interaction complement: delivery requires a real-time human (score 2) |
| `m3` | sign-off complement: a licensed human reviews or signs (score 3) |
| `C` | total complement margin, m2 + m3 |
| `I` | inert margin: physical / on-site / sensory tasks AI cannot perform (score 1) |
| `C_star` | Workflow Completeness ceiling: S + (2/3)·m3 + (1/3)·m2 |
| `n_tasks` | number of scored task statements |

S + C + I = 1 by construction. Aggregation is importance-weighted (O*NET scale IM).

**`data/tasks.csv`**: one row per (occupation, task): SOC code, task ID, task statement, O*NET importance, the 1–4 score under each of the six raters, and the incumbent rater's one-line grading rationale (`reason_sonnet_4`).

**`data/occupations_by_rater.csv`**: the occupation margins recomputed under each rater separately (798 × 6 rows), for stability checks.

## Construction, in three sentences

Each O*NET task statement is graded on one question: what does the task require of a human? A task scores 1 if it requires physical manipulation, on-site presence, or sensory inspection; non-physical tasks score 2 (real-time human delivery), 3 (sign-off under external rules), or 4 (the cognitive output is the deliverable). The criterion reads a structural property of the task rather than judging model capability, which is why six models from four developers agree unanimously on 82% of tasks (Cramér's V = 0.030 on the physical/cognitive binary).

The exact scoring prompt, raw model outputs, and full replication code are archived at **doi.org/10.5281/zenodo.21420713**.

## Employment weights

The file ships without employment counts so it never goes stale. To weight by employment, merge `soc6` against BLS OEWS national data (any vintage) on `OCC_CODE`.

## Citing

If you use these scores, please cite:

- Verschuere, B. and A. Cameron, “Hiding in the Mean: The Two Margins of AI’s Employment Effect” (SSRN 7195359) — the margins and their employment effects.
- Verschuere, B. and A. Cameron, “The Two Axes That Sort AI Use: Task-Level Evidence from Platform Usage Logs” (SSRN 7408558; under review, PNAS Nexus) — the measure’s construction, rater stability, validation, and usage evidence.
- Verschuere, B. and A. Cameron, “A Protocol for Rater-Invariant Measures from Language Models, with an Application to AI Exposure” (SSRN 7114299; 2026 Conference on Frontiers in Machine Learning and Economics, Federal Reserve Bank of Philadelphia and Chicago Booth) — the measurement protocol.

License: **CC BY 4.0**. Use freely, attribute. We would genuinely like to hear about results built on these scores, including results that break them: ben.verschuere@liminal-capital.com

*Liminal Capital Research. O*NET data are sponsored by the US Department of Labor (public domain, used per O*NET license terms).*
