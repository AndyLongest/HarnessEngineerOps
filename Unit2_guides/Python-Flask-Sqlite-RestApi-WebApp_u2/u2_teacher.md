# Python-Flask-Sqlite-RestApi-WebApp Unit 2 Teacher Guide

## 教师结论

中等偏复杂 Flask 仓库，必须用 scope。不要要求学生解释整个仓库，应限定 Setup/Admin/Apply/Model API 主线。

## 课堂重点

- 规模：约 85 个 tracked files。
- 证据：`README.md`、`server.py`、`settings.py`、`database.py`、`models.py`、`pages.py`、`forms.py`、`api/sources.py`、`requirements.txt`。
- 失败点：被 DevOps 图吸走；漏首次 `/` setup；漏 `server.py` 中 `init_db()`；混淆 admin/guest；漏 API 挂载。

## 推荐学生新增工件

`scope_contract.md`、`AGENTS.md`、`RUNBOOK.md`、`PROJECT_MAP.md`、`DATA_MODEL.md`、`FLOW_SETUP_ADMIN_MODEL_API.md`、`SMOKE_TEST.md`、`KNOWN_RISKS.md`。

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

## Harness Design Tradeoff 教师观察点

观察学生是否把 Unit2 理解成“最小可用冷启动地图”，而不是“文档越多越好”。重点看：`AGENTS.md` 是否短入口而非百科全书；`PROJECT_MAP.md` 是否导航核心路径而非复制完整文件树；专题文档是否压缩业务对象、启动、风险和 smoke 路径；新增文档是否让 final Agent 少猜、少误判、少依赖口头补充。

教师还应引导学生区分软约束和硬约束：Unit2 的入口文档、运行手册、风险提示多数只能降低误读，不能强制 Agent 不越界；需要强制执行的边界应留到 Unit3 变成 allowed/forbidden files、permission matrix 或 approval stop。

正式评分应把 Harness 完整度和 Harness 有效度分开：完整度看必要工件是否存在并包含关键部分；有效度看冷启动输出、文件读取路径、误判、不确定表达和 Harness-first routing 是否真的改善。文档过长、过碎或复述源码，只有在证据显示它降低冷启动质量时才作为有效度问题。
## 评分提醒

不要按 Markdown 数量给分。高分答案应尊重 scope，并能解释 setup/admin/model API 风险。
