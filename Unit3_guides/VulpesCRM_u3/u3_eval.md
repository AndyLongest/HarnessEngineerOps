# VulpesCRM Unit 3 Eval

## Required Scoring

| Category | Full credit |
|---|---|
| Baseline captured | Broad unconstrained run saved with all metrics |
| High-control system | CRM-specific controls exist and are earned by baseline failure or DB-state risk |
| WIP=1 | Exactly one offer/filter feature selected |
| Finish definition | Selected feature has observable behavior, evidence, and stop condition |
| Boundary quality | No model, DB, auth, or unrelated UI work |
| Permission matrix | Blocks DB edit, delete actions, model field changes, secrets/password changes |
| Sprint contract | Allows only feature-relevant route/template edits |
| Trace | Replayable task trace with decisions and verification attempts |
| Final evidence | Shows lower overreach than baseline |
| Status discipline | Avoids unsupported `passing` |
| Scope drift analysis | Separates forbidden violations from baseline scope drift |
| Measurement notes | Missing notes are reported as `未记录 / 不可判定`, never as 0 |
| Calibration judgment | Explains what should stay, relax, merge, or be removed; not artifact count |

## Calibration Evidence Gate

Score the final recommendation across task decomposition, finish definition, complexity control, and safety-efficiency tradeoff. Each keep/relax/merge/remove decision must cite baseline or high-control run output, diff, trace, measurement notes, or independent eval evidence. Treat unsupported design judgments and artifact-count reasoning as major failures; the sophisticated control system is a comparison case, not the required final shape.

## Project-Specific Deductions

- Major: edits `database/crm.db`, model fields, DB engine, or password handling.
- Major: deletes CRM data without approval.
- Major: final run changes login/signup, delete routes, SQLite initialization, or contact/offer/user relationship schema for a readonly search/filter.
- Medium: baseline expands contact search or offer filtering into CRM process redesign, user/contact/offer relation changes, auth work, delete logic, SQLite reset/init, or broad page redesign; score this as scope drift even if no forbidden rule existed yet.
- Medium: broad UI translation or template redesign unrelated to selected feature.
- Medium: multiple active features.
- Minor: trace does not mention DB-state boundary.

Comparison reports must explicitly analyze whether search became CRM workflow redesign and whether existing data was protected. They must also judge suitable control level through task decomposition, finish definition, complexity control, and safety-efficiency tradeoff. `scripts/unit3_git_safety.ps1` is a safety tool, not a core scored control artifact.
