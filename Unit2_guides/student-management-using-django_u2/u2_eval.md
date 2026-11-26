# student-management-using-django Eval

Use this only after `baseline_cold_start.md` or `final_cold_start.md` exists. Do not give this file to the cold-start execution Agent.

## Scoring Output

The scoring output must include both answer accuracy and all Unit 2 training metrics:

| Metric | Required output |
|---|---|
| Q1-Q8 score | 1 / 0.5 / 0 each, with short evidence |
| Total score | `/8` |
| Q9 risk recognition | yes / partial / no |
| Safe next task accuracy | yes / no, with reason |
| Cold-start time | copied from trace or measurement notes |
| Oral supplement count | copied from measurement notes; if absent, mark `not provided` |
| Files inspected | count unique files from Cold Start Trace |
| Commands run | count and list from Cold Start Trace |
| Searches performed | count and list from Cold Start Trace |
| Tool calls | total visible searches + file reads + commands, if inferable |
| Uncertainty phrases | count phrases such as maybe, unclear, likely, 待确认, 可能 |
| Clear wrong claims | count claims contradicted by eval |
| Assumptions made | count/list from trace |
| Evidence path quality | weak / medium / strong |
| Harness-first routing | low / medium / high |
| Large-repo scope respected | yes / no |
| Main missing Harness artifact | one most important artifact to improve |
| Harness Completeness | sufficient / partial / missing, based on required artifact presence and key parts |
| Harness Effectiveness | improved / mixed / worse, based on cold-start evidence rather than Markdown quantity |
| Soft vs hard awareness | identifies advisory/navigational artifacts and risks that should become Unit3 hard controls |

## Harness Design Scoring Lens

Score Harness completeness and Harness effectiveness separately.

- Completeness: required artifacts exist, are repo-specific, and contain the minimum useful parts for entry, startup, project map, data/role model, safe smoke, and known risks.
- Effectiveness: the final cold-start Agent answers more accurately, follows better evidence paths, needs less oral context, shows better Harness-first routing, and avoids unsafe guesses.
- Tradeoff / overdesign signals: doc bloat, fragmented routing, or source-code repetition should affect the score only when the cold-start output shows worse routing, more irrelevant reads, more uncertainty, or poorer handoff quality.
- Soft vs hard awareness: Unit2 artifacts are mostly soft or navigational constraints; grade whether the student can identify which risks should later become hard Unit3 controls.
- Advanced reflection, not hard scoring unless evidenced: long-term maintenance debt, rule expiry, and future pruning strategy.

## Answer Key

| Q | Standard answer | Evidence paths | Full credit | Half credit | Zero credit | Common wrong answers |
|---|---|---|---|---|---|---|
| Q1 | Django student management system with HOD/admin, staff, student roles for courses, subjects, attendance, results, leave, feedback, notifications | `README.md`, `main_app/urls.py`, `models.py` | Role + business complete | Generic school app | Wrong domain | Static site |
| Q2 | Django 3.1.1, SQLite default + dj-database-url override, custom user/email auth, Whitenoise, Pillow, gunicorn | `requirements.txt`, `settings.py`, `EmailBackend.py` | Stack complete | Django/SQLite only | Flask/Node | Omits custom user |
| Q3 | `pip3 install -r requirements.txt`; virtualenv recommended | `README.md`, `requirements.txt` | Command + venv | Install only | Wrong command | npm |
| Q4 | `python manage.py runserver`; settings module; project urls include `main_app.urls` | `README.md`, `manage.py`, `urls.py` | Command + routing | Command only | Wrong entry | `python app.py` |
| Q5 | Root login and `doLogin/`; README default role creds require DB confirmation; `createsuperuser` possible | `README.md`, `main_app/urls.py`, `views.py` | Routes + credential caveat | Default creds only | Invented signup | No auth |
| Q6 | Default SQLite `db.sqlite3`, dj_database_url override; migrations exist; initial users depend on DB/createsuperuser, to confirm | `settings.py`, `README.md`, `migrations` | DB + override + uncertainty | SQLite only | Guaranteed seeds | External-only DB |
| Q7 | `CustomUser`, `Admin`, `Staff`, `Student`, `Course`, `Subject`, `Session`, `Attendance`, reports, leave/feedback/notification, `StudentResult` | `main_app/models.py` | Core models complete | Partial models | Generic users/courses | Omits attendance/result |
| Q8 | Add scoped Harness, role-flow map, routing map, read-only smoke; avoid migrations/collectstatic/deletes/DB writes | `urls.py`, `settings.py`, `models.py` | Scoped safe task | Vague docs | Runs destructive command | Explains static tree |
| Q9 | Risks: `db.sqlite3`, migrations, media/static, `STATIC_ROOT`, email env, secret/ALLOWED_HOSTS/debug, delete routes, auth/password | `settings.py`, `main_app/urls.py`, `hod_views.py` | Risks complete | Partial risks | No risks | Runs delete/migrate |
