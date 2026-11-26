# Inventory-Manager Eval

Use this only after `baseline_cold_start.md`, `detailed_doc_cold_start.md`, or `final_cold_start.md` exists. Score each run independently; do not give this file to the cold-start execution Agent.

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
| Main guidance gap | one most important repo-guidance problem to improve |

## Calibration Review

After all three runs exist, evaluate the final comparison as a design judgment, not an artifact count. Require evidence for: the baseline guidance failure, Agent abilities improved by the detailed system, costs or contradictions introduced by that system, and every final keep/merge/remove decision. A final system passes calibration only when it is safer and easier to hand off than baseline and its remaining complexity is justified against the detailed-doc run.

## Answer Key

| Q | Standard answer | Evidence paths | Full credit | Half credit | Zero credit | Common wrong answers |
|---|---|---|---|---|---|---|
| Q1 | Flask inventory/warehouse app for products, locations, transfers, balances | `README.md`, `routes.py`, `models.py` | Inventory + transfer/balance | Inventory CRUD only | Wrong domain | CRM |
| Q2 | Python Flask, Flask-SQLAlchemy, Flask-WTF/WTForms, Jinja, SQLite-like DB | `requirements.txt`, `__init__.py`, `forms.py` | Stack complete | Flask/SQLAlchemy only | Django/React | sqlite3 helper |
| Q3 | `pip3 install -r requirements.txt` | `README.md`, `requirements.txt` | Exact command | Generic pip | Wrong command | npm |
| Q4 | `python run.py` | `README.md`, `run.py` | Exact entry | Mentions run.py vaguely | Wrong entry | `python app.py` |
| Q5 | No registration/login evidence; routes appear public | `routes.py`, `README.md` | Explicit no auth evidence | Says undocumented | Invents login | Claims required auth |
| Q6 | DB configured in app init; `db.create_all()` creates tables; exact file/URI should be marked to confirm | `__init__.py`, `models.py` | create_all + uncertainty | SQLite only | Invented seed | External DB |
| Q7 | `Location`, `Product`, `Movement`, `Balance`; Movement is history, Balance is current quantity | `models.py`, `routes.py` | Models + distinction | Missing one | Generic objects | Movement=current stock |
| Q8 | Refine suitable repo guidance for transfer rules and non-destructive smoke/inspect | `routes.py`, `models.py` | Safe and specific | Vague tests/docs | Change algorithm/delete | Destructive smoke |
| Q9 | Risks: delete route, `check()` mutates Product/Balance, `db.create_all()`, DB file | `routes.py`, `__init__.py` | Mutation points complete | Partial risks | No risks | Deletes in smoke |
