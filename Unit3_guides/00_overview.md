# Unit 3 Overview: From Agent-readable to Agent-controllable

Unit 2 asked students to make a repo easier for a new Agent to understand. Unit 3 asks a different question: after an Agent can understand the repo, can the team keep the Agent inside the correct execution boundary?

Core sentence for every project:

> Unit 3 的目标是把一个 Agent-readable repo，进一步改造成 Agent-controllable repo。

## What Students Will Prove

Students must run the same repo twice:

1. Baseline unconstrained run: give the Agent a real but broad task with no `feature_list.json`, no permission matrix, no `sprint_contract.md`, and no required trace.
2. Final constrained run: repeat the same class of task after adding Unit 3 control artifacts.
3. Comparison report: determine whether overreach and out-of-scope edits decreased, WIP=1 became clearer, risky actions were blocked, and task trace quality improved. Record unchanged or worse results with the same evidence standard.

The constrained run is a high-control comparison case. Learners then justify which controls to retain, relax, merge, or remove by connecting behavior changes to task-granularity, completion-definition, complexity, and safety/efficiency costs. A final retest is useful when feasible. Record model, prompt, permission, budget, starting-state, and human-assistance differences before attributing an improvement to a control.

The output is not graded by Markdown volume. A short, enforceable control file is better than a long narrative that the Agent can ignore.

Unit 3 separates two findings:

- `forbidden violation`: the Agent broke an explicit rule that existed at the time.
- `scope drift`: the Agent expanded the work when no explicit rule had been supplied, especially during baseline.

Baseline runs should be judged primarily for scope drift. Final runs should be judged primarily for boundary compliance and whether the final comparison proves scope drift decreased.

## Safety Net

Unit 3 baseline runs will make real file changes. Because the baseline task is intentionally broad, the Agent may leave behind half-finished edits, wrong file touches, or incomplete state changes. Every group should create a rollback harness first, then verify that the Agent can use it from the chat UI: when the student asks to rollback, the Agent should save diff evidence, restore the repo, and report the clean/dirty status before final controls are built.

The rollback harness, usually `scripts/unit3_git_safety.ps1`, is an experiment safety tool. It is not a core Unit 3 control artifact for quality scoring. The core controls remain `feature_list.json`, `task_boundary.md`, `docs/policies/permission-matrix.md`, `docs/policies/human-approval-flow.md`, `sprint_contract.md`, and `logs/agent-runs/<feature-id>.md`.

## Task Design Rule

Unit 3 tasks must be understandable as teaching cases, not copied prompts. Each project guide now names:

- why the task was selected from the repo's real workflow;
- why it is broad enough to tempt Agent overreach;
- how to split it into 2-3 atomic candidate features;
- which one feature should become `active` in the final constrained run;
- what evidence would show the selected feature is ready for verification.

This follows the core Unit 3 design principles: WIP=1, externalized scope surface, feature-list triples, and observable execution traces.

Baseline prompts should sound like real product requests. They should give the Agent enough freedom to choose a surface, but should not list high-risk areas, allowed files, forbidden files, or Unit 3 control artifacts. They should still require the Agent to save implementation notes and verification records to `measurement_logs/baseline_unconstrained_run.md`, so the later eval and comparison have a stable input. Their purpose is to observe natural scope drift.

Final constrained runs must allow only one active feature. The Agent must read `feature_list.json`, sign or fill `sprint_contract.md`, cite the permission matrix, record a task trace, explain why it did not do the other candidate features, and note discovered but unfixed out-of-scope issues.

## Project Set

The Unit 3 guide set mirrors the real local `UNIT2_GUIDES` child directories:

- `Inventory-Manager`
- `issue-tracker`
- `Python-Flask-Sqlite-RestApi-WebApp`
- `student-management-using-django`
- `VulpesCRM`

## Unit 2 Summary Used For Unit 3 Design

| Project | Unit 2 scope decision | Repo risks from Unit 2 | Student intensity | Unit 3 emphasis |
|---|---|---|---|---|
| `Inventory-Manager` | Full small Flask inventory repo | Transfer writes inventory state; `Movement` vs `Balance`; delete route; `db.create_all()` | Weak group | Prevent small-repo overreach and casual state mutation |
| `issue-tracker` | Full small/medium Flask issue tracker | Auth, sharing permissions, REST API, `items.db`, delete/update/unshare | Weak to medium group | Keep one permission/API feature active and block DB/reset shortcuts |
| `VulpesCRM` | Full small/medium Flask CRM | `database/crm.db`, delete routes, startup `create_all`, password/auth assumptions | Medium group | Control DB-state assumptions and avoid broad translation/refactor work |
| `Python-Flask-Sqlite-RestApi-WebApp` | Scoped repo only: setup/admin/apply/model API | Large-ish Flask app; `DevOps/` distraction; admin writes, uploads, mail, DB init/delete | Medium to strong group | Use scope contract plus sprint contract to stop whole-repo exploration |
| `student-management-using-django` | Large repo scoped to Django control plane and three role flows | 3000+ static/vendor files, migrations, collectstatic, DB/media/static, auth/password | Strong group | WIP=1 plus file allowlist/denylist, especially against static/vendor drift |

## Required Deliverables Per Project

Each project guide asks students to produce:

- `measurement_logs/baseline_unconstrained_run.md`
- `scripts/unit3_git_safety.ps1`
- `measurement_logs/unit3_run_diff.patch`
- `measurement_logs/baseline_eval.md`
- `feature_list.json`
- `task_boundary.md`
- `docs/policies/permission-matrix.md`
- `docs/policies/human-approval-flow.md`
- `sprint_contract.md`
- `logs/agent-runs/<feature-id>.md`
- `measurement_logs/final_constrained_run.md`
- `measurement_logs/final_eval.md`
- `measurement_logs/unit3_comparison_report.md`

## Do Not Drift Into Unit 4

Unit 3 stops at controllability evidence. Do not add Completion Gate, E2E gate design, final handoff protocol, release signoff, or long-term ownership workflow. Those belong later.
