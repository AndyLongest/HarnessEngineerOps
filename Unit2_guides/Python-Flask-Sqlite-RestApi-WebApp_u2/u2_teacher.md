# Python-Flask-Sqlite-RestApi-WebApp Unit 2 Teacher Guide

## 教师结论

中等偏复杂 Flask 仓库，必须用 scope。不要要求学生解释整个仓库，应限定 Setup/Admin/Apply/Model API 主线。

## 课堂重点

- 规模：约 85 个 tracked files。
- 证据：`README.md`、`server.py`、`settings.py`、`database.py`、`models.py`、`pages.py`、`forms.py`、`api/sources.py`、`requirements.txt`。
- 失败点：被 DevOps 图吸走；漏首次 `/` setup；漏 `server.py` 中 `init_db()`；混淆 admin/guest；漏 API 挂载。

## 候选 Harness 组件

这些是候选组件，不是标准答案：`scope_contract.md`、`AGENTS.md`、`RUNBOOK.md`、`PROJECT_MAP.md`、`DATA_MODEL.md`、`FLOW_SETUP_ADMIN_MODEL_API.md`、`SMOKE_TEST.md`、`KNOWN_RISKS.md`。

学生应先比较 baseline、detailed-doc、final 三次冷启动，再解释最终保留哪些文档以及为什么。

## Eval：标准答案和评分规则

| Q | 标准答案 | 证据路径 | 满分 | 半分 | 零分 | 常见错答 |
|---|---|---|---|---|---|---|
| Q1 | Flask casting agency，管理 agency、models/actors、applications、admin panel、model API | `README.md`, `server.py`, `pages.py`, `models.py` | 说出 casting agency+admin/API | generic Flask site | 领域错 | CRM |
| Q2 | Flask, Flask-Admin, Flask-Security/Login, Flask-Mail, Flask-RESTful, SQLAlchemy, SQLite, WTForms | `requirements.txt`, `server.py`, `forms.py` | 栈完整 | Flask/SQLite 部分 | Django/React | 漏 Security |
| Q3 | `pip install -r requirements.txt`，并检查 `settings.py` 邮件配置 | `README.md`, `requirements.txt`, `settings.py` | 命令+配置提醒 | 只有安装 | 错命令 | npm |
| Q4 | `python server.py`；默认 localhost:3000；启动调用 `init_db()` | `README.md`, `server.py`, `settings.py` | 命令+端口+init | 只有命令 | 错入口 | app.py |
| Q5 | `/` setup 创建 admin/app；`/admin-login` admin；`/signup`/`/login` guest/company | `pages.py`, `forms.py`, `settings.py` | 区分流程 | 只说 login/signup | 编造固定账号 | 无认证 |
| Q6 | SQLite `softwareEng.db`；`database.py` engine；`init_db()` 建表；初始内容待确认 | `settings.py`, `database.py`, `server.py` | DB+init+未知边界 | SQLite only | seed script | 外部 DB |
| Q7 | Setup, User, Role, Agency, Categories, Actors, ActorBody, ActorSoul, Photos, TempActors 系列, NormalContact | `models.py` | scoped 对象完整 | 漏 temp/apply | 泛泛 users/items | 无 API 对象 |
| Q8 | 安全下一步：补 scoped Harness 和只读 smoke；避免 DB init/delete/upload/mail 写 | `server.py`, `pages.py`, `database.py` | scoped 非破坏 | 泛泛 docs | 调 delete_db/上传 | 全仓库解释 |
| Q9 | 风险：`softwareEng.db`、`init_db/delete_db`、admin writes、uploads、mail、secret/debug、空 mail/recaptcha | `database.py`, `server.py`, `pages.py`, `settings.py` | 风险完整 | 只说 secret | 无风险 | setup 当只读 |

## 独立评分流程

执行 Agent 不看 eval；评分 Agent 只看 eval 和输出。评分时不因学生未解释 scope 外 DevOps 全部资料扣分。

## 指标提取

除常规指标外，记录“是否遵守 scope”。文件数不一定下降，阅读路径必须变好。

## 评分提醒

不要按 Markdown 数量给分。高分答案应尊重 scope，并能解释 setup/admin/model API 风险。教师可从 cold-start trace、eval、对比报告和文档变更中判断学生是否经历了“发现缺口、尝试详细系统、识别成本、再平衡”的过程。
