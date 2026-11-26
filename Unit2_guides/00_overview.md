# Unit 2 Guide Package Overview

Unit 2 的目标不是生成更多 Markdown，而是让一个全新的 Agent 在冷启动前后表现出可测量改善：更快理解仓库、更少猜测、更少口头补充、更能识别安全下一步任务。核心转变是：从“源码侦察”变成“Harness 路由 + 定向核验”。

| Repo | Type | Size judgment | Scope needed? | Unit2 training focus | Risk |
|---|---|---|---|---|---|
| VulpesCRM | Flask + SQLAlchemy + SQLite CRM | Small-medium, 26 tracked files | Full repo is acceptable | Explain CRM offer/contact/user flow, database location, login/signup, safe smoke path | Existing SQLite database and delete routes; `main.py` creates tables on startup |
| issue-tracker | Flask + sqlite3 + Flask-Login task tracker | Small, 24 tracked files | Full repo is acceptable | Explain task ownership, sharing permissions, API routes, Docker option | `app.py` initializes/updates `items.db`; delete/update routes mutate demo data |
| Inventory-Manager | Flask + Flask-SQLAlchemy inventory app | Small, 12 tracked files | Full repo is acceptable | Explain product/location/movement/balance model and transfer invariants | Importing app creates tables; transfer logic mutates stock balances |
| Python-Flask-Sqlite-RestApi-WebApp | Flask casting agency + admin + REST API | Medium, 85 tracked files | Scope recommended | Scope to startup, setup/admin, model application, model API, core tables | `server.py` calls `init_db()`; setup/admin path and mail/upload config are easy to misread |
| student-management-using-django | Django student management system | Large, 3688 tracked files, mostly static/vendor assets | Scope required | Scope to startup/auth, three-role routing, HOD management, staff attendance/result, student read-only views | Static/vendor noise, migrations, media/static output, email/env settings, destructive delete views |

## Group Recommendations

Weak groups: `Inventory-Manager` or `issue-tracker`. They have fewer files and clear business objects, so students can see metric improvement quickly.

Medium groups: `VulpesCRM` or scoped `Python-Flask-Sqlite-RestApi-WebApp`. These require better routing through login, database, and business flows.

Strong groups: scoped `student-management-using-django`. The challenge is not explaining everything; it is writing a scope contract that helps an Agent ignore thousands of irrelevant static/vendor files and route to the correct Django modules.

## Shared Reminder

Do not compare raw file counts or cold-start times across repositories. Compare baseline vs final only inside the same repository.

## Harness Design Tradeoff Reminder

Unit 2 still asks students to build a minimal usable cold-start harness. The new design lens is not "write more docs"; it is "write just enough compressed guidance for a new Agent to find the right path."

Unit 2 also introduces the vocabulary for soft constraints and hard constraints, but it does not add a formal soft-vs-hard experiment. Most Unit 2 artifacts are soft or navigational constraints: `AGENTS.md`, `RUNBOOK.md`, `PROJECT_MAP.md`, and `KNOWN_RISKS.md` can reduce misreading and unsafe guesses, but they cannot force an Agent to stay inside a boundary.

Use this distinction only as a reflection lens in Unit 2. Students should be able to say which information is merely advisory, and which information starts to look like an enforceable boundary that belongs in Unit 3.

Students should experience two common tradeoffs:

- One giant document vs too many fragmented documents.
- Information too brief vs information copied without compression.

Student guides should keep this lightweight and place the main reflection in the final comparison report. Teacher guides and eval files should carry the deeper design judgment: whether the added artifacts improved cold-start behavior, or whether they only increased harness completeness while lowering harness effectiveness.
