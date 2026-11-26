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

本轮实践比较 baseline、准确但详细的文档版本和改进后的 final。学生需要解释文档如何改变 Agent 的读取、判断和风险识别，同时评估重复、维护和人工复核成本。最终设计由运行证据支持。

Do not compare raw file counts or cold-start times across repositories. Compare baseline vs final only inside the same repository.
