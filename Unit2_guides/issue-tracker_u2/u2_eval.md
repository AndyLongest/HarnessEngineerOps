# issue-tracker Eval

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
| Q1 | Flask issue/task tracker with auth, CRUD, comments, sharing permissions, REST API | `README.md`, `app.py`, `api.py` | Task tracker + sharing/API | CRUD only | Wrong domain | CRM |
| Q2 | Flask, Flask-Login, Flask-RESTful, sqlite3/SQLite, bcrypt, Jinja, optional Docker | `requirements.txt`, `app.py`, `api.py` | Stack complete | Flask/SQLite only | Invented ORM/Django | SQLAlchemy |
| Q3 | `pip install -r requirements.txt` | `README.md`, `requirements.txt` | Exact command | Generic pip | Wrong command | Docker only |
| Q4 | `python app.py` on port 5000; Docker Compose optional | `README.md`, `app.py`, `docker-compose.yml` | Local + optional Docker | One valid path | Wrong entry | `flask run` only |
| Q5 | `/register`, `/login`, `/logout`; bcrypt password hashing | `app.py`, templates | Routes + hashing | Routes only | Invented default users | No auth |
| Q6 | SQLite `items.db`; schema/helper in `db.py`; `init_db()` creates missing tables | `db.py`, `app.py` | File + init behavior | SQLite only | External DB | Treats DB as cache |
| Q7 | `users`, `items`, `notes`, `task_shares`; owner/shared permissions with edit flags | `db.py`, `app.py` | Tables + permission fields | Users/items only | Generic objects | Omits `task_shares` |
| Q8 | Add Harness docs, API map, permission smoke, read-only DB inspect | `app.py`, `db.py`, `api.py` | Safe and specific | Vague tests/docs | Reset/delete DB | Migration first |
| Q9 | Risks: `items.db`, `init_db()`, delete/update/unshare, sharing permissions, random secret/session | `db.py`, `app.py` | DB + destructive + permissions | Partial risks | No risks | Delete in smoke |
