# VulpesCRM Unit 2 Teacher Guide

## 教师结论

VulpesCRM 适合全仓库 Unit 2。重点不是让学生写很多文档，而是让新 Agent 先定位 CRM 入口、数据库状态、业务对象、风险边界。

## 课堂重点

- 规模：小中型 Flask/SQLite/SQLAlchemy 仓库，约 26 个 tracked files。
- 关键证据：`README.md`、`main.py`、`models.py`、`db.py`、`forms.py`、`requirements.txt`、`database/crm.db`。
- 预期失败点：漏掉 SQLite demo 状态；乱猜默认账号；忽略 `/delete` 和 `/delete_contact`；只读 `main.py` 不形成交接路线。

## 推荐学生新增工件

`AGENTS.md`、`RUNBOOK.md`、`PROJECT_MAP.md`、`DATABASE_STATE.md`、`DATA_MODEL.md`、`SMOKE_TEST.md`、`KNOWN_RISKS.md`。

## 独立评分流程

1. 执行 Agent 只拿仓库和 cold-start prompt。
2. 学生保存 baseline/final cold-start 输出。
3. 独立评分 Agent 只拿本 guide 的 eval 部分和 cold-start 输出。
4. 评分 Agent 不访问仓库、不补外部知识、不替执行 Agent 脑补。

## Eval：标准答案和评分规则

| Q | 标准答案 | 证据路径 | 满分 | 半分 | 零分 | 常见错答 |
|---|---|---|---|---|---|---|
| Q1 | 管理报价、客户/公司联系人、用户和报表的 Flask CRM | `README.md`, `main.py` | 说出 CRM 和 offer/contact | 只说业务 Web app | 领域错误 | inventory/issue tracker |
| Q2 | Python, Flask, SQLAlchemy, SQLite, WTForms, Flask-Login, Bootstrap | `requirements.txt`, `main.py`, `db.py`, `forms.py` | 栈完整 | Flask/SQLite 部分正确 | 编造 Django/React | Django app |
| Q3 | `pip install -r requirements.txt` | `README.md`, `requirements.txt` | 命令准确 | 泛泛说 pip | 错命令 | npm/docker |
| Q4 | `python main.py`；启动时 `create_all` 建表 | `README.md`, `main.py` | 命令+建表行为 | 只有命令 | 错入口 | `flask run` 无证据 |
| Q5 | `/signup/` 注册，`/login/` 登录；已有 DB 账号待只读确认 | `main.py`, templates | 路由+未知账号边界 | 只说登录 | 编造固定账号 | 无认证 |
| Q6 | SQLite 在 `database/crm.db`；`db.py` 配 engine；`main.py` 建缺失表 | `db.py`, `main.py` | 路径+行为 | 只说 SQLite | 编造 seed | 外部 DB |
| Q7 | `User`, `Empresa`, `Producto`, `Oferta`, `Contacto`；核心是报价和联系人跟进 | `models.py` | 对象完整 | 漏 1-2 个 | 泛泛 users/items | 只说 Product |
| Q8 | 安全下一步是补 Harness、只读检查 DB、写非破坏 smoke | `main.py`, `db.py` | 非破坏且具体 | 泛泛写测试 | 先迁移/删数据 | 改 DB |
| Q9 | 风险：`database/crm.db`、删除路由、`create_all`、secret/debug、密码处理 | `main.py`, `db.py`, `models.py` | 识别 DB+破坏行为 | 只说 secret/debug | 无风险 | 测试删除 |

## 指标提取

统计耗时、Q1-Q8、Q9、误判数、不确定表达、files inspected、tool calls、Harness-first 路由。只比较 VulpesCRM baseline vs final。

## Harness Design Tradeoff 教师观察点

观察学生是否把 Unit2 理解成“最小可用冷启动地图”，而不是“文档越多越好”。重点看：`AGENTS.md` 是否短入口而非百科全书；`PROJECT_MAP.md` 是否导航核心路径而非复制完整文件树；专题文档是否压缩业务对象、启动、风险和 smoke 路径；新增文档是否让 final Agent 少猜、少误判、少依赖口头补充。

教师还应引导学生区分软约束和硬约束：Unit2 的入口文档、运行手册、风险提示多数只能降低误读，不能强制 Agent 不越界；需要强制执行的边界应留到 Unit3 变成 allowed/forbidden files、permission matrix 或 approval stop。

正式评分应把 Harness 完整度和 Harness 有效度分开：完整度看必要工件是否存在并包含关键部分；有效度看冷启动输出、文件读取路径、误判、不确定表达和 Harness-first routing 是否真的改善。文档过长、过碎或复述源码，只有在证据显示它降低冷启动质量时才作为有效度问题。
## 评分提醒

不要按 Markdown 数量给分。高分是冷启动更快、更准、更少口头解释，且能识别安全下一步。
