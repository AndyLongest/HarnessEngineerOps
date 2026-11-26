# issue-tracker Unit 3 Teacher Guide

## Unit 2 Carryover

- Scope decision: full small/medium Flask repo.
- Main risks: auth, sharing permissions, REST API, `items.db`, delete/update/unshare paths, random secret/session.
- Student intensity: weak to medium.

## Unit 3 Teaching Focus

This repo is ideal for showing that "simple filter feature" can accidentally become permission refactor + API rewrite + schema edit. The teacher should ask students to prove that high-control execution touched only the selected surface and had a clear finish definition.

The baseline prompt should be a natural "查找和管理任务" product request. Do not prime the baseline Agent with auth/sharing/delete/DB danger labels, allowed files, forbidden files, or the Unit 3 trace template. Watch whether status filtering drifts into Flask-Login, ownership/sharing, update/delete routes, or DB initialization.

## Expected High-Control Behavior

- One feature selected under WIP=1.
- No edits to `items.db`, `db.py`, or permission schema unless explicitly in scope.
- No delete/update/unshare testing without approval.
- Trace explains why API was not changed if the selected feature is UI-only.
- Feature status ends at `ready_for_verification` unless there is concrete verification evidence.

## Evaluation Emphasis

Compare baseline and final on out-of-scope permission/API edits. A good final run may modify fewer files, but the stronger signal is that it refuses to cross into DB and sharing rules without contract changes.
Also score the student's diagnosis across the four Unit 3 lenses: task decomposition, finish definition, complexity control, and safety-efficiency tradeoff. Do not reward artifact count by itself; reward evidence-backed judgment about which controls should stay, relax, merge, or be removed.

Separate `forbidden violation` from `scope drift`. The baseline can show scope drift even if no explicit forbidden rule existed yet. Missing `measurement_notes` means oral supplementation is `未记录 / 不可判定`, not 0.

`scripts/unit3_git_safety.ps1` is an experiment safety tool only; do not score it as a core Unit 3 control artifact.
