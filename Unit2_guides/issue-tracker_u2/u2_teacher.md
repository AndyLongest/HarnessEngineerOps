# issue-tracker Unit 2 Teacher Guide

## 教师结论

适合弱/中等组。文件少但权限模型完整，能训练学生让 Agent 准确理解所有权、共享、API 和数据库风险。

## 课堂重点

- 规模：约 24 个 tracked files，全仓库 Unit 2。
- 证据：`README.md`、`app.py`、`db.py`、`api.py`、`requirements.txt`、`Dockerfile`、`docker-compose.yml`、`items.db`。
- 失败点：只说 CRUD；漏 `task_shares`；漏 API；把 `items.db` 当缓存；忽略 delete/update/unshare 风险。

## 推荐学生新增工件

`AGENTS.md`、`RUNBOOK.md`、`PROJECT_MAP.md`、`DATA_MODEL.md`、`API_MAP.md`、`SMOKE_TEST.md`、`KNOWN_RISKS.md`。

## Eval：标准答案和评分规则

| Q | 标准答案 | 证据路径 | 满分 | 半分 | 零分 | 常见错答 |
|---|---|---|---|---|---|---|
| Q1 | Flask issue/task tracker，含认证、任务 CRUD、评论、共享权限、REST API | `README.md`, `app.py`, `api.py` | 说出任务跟踪+共享/API | 只说 CRUD | 领域错 | CRM |
| Q2 | Python Flask, Flask-Login, Flask-RESTful, sqlite3/SQLite, bcrypt, Jinja, optional Docker | `requirements.txt`, `app.py`, `api.py` | 栈完整 | Flask/SQLite 部分 | 编造 ORM/Django | SQLAlchemy |
| Q3 | `pip install -r requirements.txt` | `README.md`, `requirements.txt` | 命令准确 | 泛泛 pip | 错命令 | Docker only |
| Q4 | `python app.py`，端口 5000；Docker Compose 可选 | `README.md`, `app.py`, `docker-compose.yml` | 本地+可选 Docker | 只有一个有效路径 | 错入口 | flask run only |
| Q5 | `/register` 注册，`/login` 登录，bcrypt 哈希 | `app.py`, templates | 路由+哈希 | 只说路由 | 编造默认用户 | 无认证 |
| Q6 | SQLite `items.db`；`db.py` 定义 schema；启动时 `init_db()` 建缺失表 | `db.py`, `app.py` | 路径+init 行为 | 只说 SQLite | 外部 DB | 缓存 |
| Q7 | `users`, `items`, `notes`, `task_shares`；owner/shared 权限字段 | `db.py`, `app.py` | 表+权限完整 | 漏共享权限 | 泛泛 users/items | 无 task_shares |
| Q8 | 安全下一步：补 Harness、API map、权限 smoke；只读检查 DB | `app.py`, `db.py`, `api.py` | 非破坏且具体 | 泛泛测试 | 删除/重置 DB | 先迁移 |
| Q9 | 风险：`items.db`、`init_db()`、delete/update/unshare、权限逻辑、随机 secret/session | `db.py`, `app.py` | DB+破坏路由+权限 | 只说 DB | 无风险 | smoke 调 delete |

## 独立评分流程

执行 Agent 不看 eval。评分 Agent 只看 eval 和 cold-start 输出，不访问仓库。

## 指标提取

Q1-Q8、Q9、误判、不确定表达、文件数、工具数、Harness-first 路由。只比较本仓库前后。

## Harness Design Tradeoff 教师观察点

观察学生是否把 Unit2 理解成“最小可用冷启动地图”，而不是“文档越多越好”。重点看：`AGENTS.md` 是否短入口而非百科全书；`PROJECT_MAP.md` 是否导航核心路径而非复制完整文件树；专题文档是否压缩业务对象、启动、风险和 smoke 路径；新增文档是否让 final Agent 少猜、少误判、少依赖口头补充。

教师还应引导学生区分软约束和硬约束：Unit2 的入口文档、运行手册、风险提示多数只能降低误读，不能强制 Agent 不越界；需要强制执行的边界应留到 Unit3 变成 allowed/forbidden files、permission matrix 或 approval stop。

正式评分应把 Harness 完整度和 Harness 有效度分开：完整度看必要工件是否存在并包含关键部分；有效度看冷启动输出、文件读取路径、误判、不确定表达和 Harness-first routing 是否真的改善。文档过长、过碎或复述源码，只有在证据显示它降低冷启动质量时才作为有效度问题。
## 评分提醒

不要按 Markdown 数量给分。高分应能准确解释 `task_shares` 和安全边界。
