# VulpesCRM Eval

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
| Q1 | Flask CRM for offers, companies/customers, contacts, users, reports | `README.md`, `main.py` | CRM + offer/contact flow | Generic business app | Wrong domain | Inventory/issue tracker |
| Q2 | Python, Flask, SQLAlchemy, SQLite, WTForms, Flask-Login, Bootstrap | `requirements.txt`, `main.py`, `db.py`, `forms.py` | Main stack complete | Flask/SQLite only | Invented stack | Django/React |
| Q3 | `pip install -r requirements.txt` | `README.md`, `requirements.txt` | Exact command | Generic pip | Wrong command | npm/docker |
| Q4 | `python main.py`; startup calls `create_all` | `README.md`, `main.py` | Command + table-create note | Command only | Wrong entry | `flask run` without evidence |
| Q5 | `/signup/` register, `/login/` login; existing DB users must be confirmed read-only | `main.py`, templates | Routes + credential uncertainty | Login only | Invented fixed creds | No auth |
| Q6 | SQLite at `database/crm.db`; engine in `db.py`; missing tables created by `main.py` | `db.py`, `main.py` | Path + behavior | SQLite only | Invented seed | External DB |
| Q7 | `User`, `Empresa`, `Producto`, `Oferta`, `Contacto`; offer/contact follow-up is core | `models.py` | All core models + flow | Some models | Generic objects | Product only |
| Q8 | Refine suitable repo guidance, read-only DB inspect, non-destructive smoke | `main.py`, `db.py` | Safe and specific | Vague tests/docs | Mutate DB first | Delete/migrate |
| Q9 | Risks: `database/crm.db`, delete routes, `create_all`, secret/debug, password handling | `main.py`, `db.py`, `models.py` | DB + destructive + config risks | Partial risks | No risks | Calls delete route |
