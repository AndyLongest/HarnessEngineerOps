# Python-Flask-Sqlite-RestApi-WebApp Eval

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
| Scope respected | yes / no |
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
| Q1 | Flask casting agency app for agency, actors/models, applications, admin panel, model API | `README.md`, `server.py`, `pages.py`, `models.py` | Casting agency + admin/API | Generic Flask site | Wrong domain | CRM |
| Q2 | Flask, Flask-Admin, Flask-Security/Login, Flask-Mail, Flask-RESTful, SQLAlchemy, SQLite, WTForms | `requirements.txt`, `server.py`, `forms.py` | Stack complete | Flask/SQLite only | Django/React | Omits Security |
| Q3 | `pip install -r requirements.txt`; check `settings.py` mail config | `README.md`, `requirements.txt`, `settings.py` | Install + config note | Install only | Wrong command | npm |
| Q4 | `python server.py`; localhost:3000; startup calls `init_db()` | `README.md`, `server.py`, `settings.py` | Command + port + init | Command only | Wrong entry | `python app.py` |
| Q5 | `/` setup creates admin/app; `/admin-login`; `/signup` and `/login` for guest/company | `pages.py`, `forms.py`, `settings.py` | Distinguishes flows | Login/signup only | Invented creds | No auth |
| Q6 | SQLite `softwareEng.db`; `database.py` engine; `init_db()` creates tables; initial content to confirm | `settings.py`, `database.py`, `server.py` | DB + init + uncertainty | SQLite only | Invented seed | External DB |
| Q7 | `Setup`, `User`, `Role`, `Agency`, `Categories`, `Actors`, actor body/soul/photos, temp actor tables, `NormalContact` | `models.py` | Scoped objects complete | Missing temp/apply | Generic objects | No API objects |
| Q8 | Add scoped Harness and read-only smoke; avoid DB init/delete/upload/mail writes | `server.py`, `pages.py`, `database.py` | Scoped safe task | Vague docs | Calls `delete_db`/uploads | Full-repo explanation |
| Q9 | Risks: `softwareEng.db`, `init_db/delete_db`, admin writes, uploads, mail, secret/debug, empty mail/recaptcha | `database.py`, `server.py`, `pages.py`, `settings.py` | Risks complete | Partial risks | No risks | Treats setup as read-only |
