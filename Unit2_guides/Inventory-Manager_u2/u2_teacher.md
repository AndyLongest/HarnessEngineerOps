# Inventory-Manager Unit 2 Teacher Guide

## 教师结论

适合弱组。仓库小，但库存转移规则能清楚展示 Harness 的价值：让 Agent 少猜业务状态变化。

## 课堂重点

- 规模：约 12 个 tracked files，全仓库 Unit 2。
- 证据：`README.md`、`run.py`、`flaskinventory/__init__.py`、`routes.py`、`models.py`、`forms.py`、`requirements.txt`。
- 失败点：编造登录；漏 `Balance`；忽略 `db.create_all()`；不理解转移会写库存。

## 推荐学生新增工件

`AGENTS.md`、`RUNBOOK.md`、`PROJECT_MAP.md`、`DATA_MODEL.md`、`TRANSFER_RULES.md`、`SMOKE_TEST.md`、`KNOWN_RISKS.md`。

## Eval：标准答案和评分规则

| Q | 标准答案 | 证据路径 | 满分 | 半分 | 零分 | 常见错答 |
|---|---|---|---|---|---|---|
| Q1 | Flask 库存/仓库系统，管理产品、位置、转移和余额 | `README.md`, `routes.py`, `models.py` | 说出库存+转移/余额 | 只说库存 CRUD | 领域错 | CRM |
| Q2 | Python Flask, Flask-SQLAlchemy, Flask-WTF/WTForms, Jinja, SQLite-like DB | `requirements.txt`, `__init__.py`, `forms.py` | 栈完整 | Flask/SQLAlchemy | Django/React | sqlite3 helper |
| Q3 | `pip3 install -r requirements.txt` | `README.md`, `requirements.txt` | 命令准确 | 泛泛 pip | 错命令 | npm |
| Q4 | `python run.py` | `README.md`, `run.py` | 入口准确 | 提到 run.py 不清楚 | 错入口 | app.py |
| Q5 | 无注册/登录证据，路由公开 | `routes.py`, `README.md` | 明确无证据 | 说未记录 | 编造登录 | 必须登录 |
| Q6 | DB 在 app 初始化中配置，`db.create_all()` 创建表；具体文件名/URI需标待确认 | `__init__.py`, `models.py` | create_all+不确定边界 | 只说 SQLite | 编造 seed | 外部 DB |
| Q7 | `Location`, `Product`, `Movement`, `Balance`；Movement 历史，Balance 当前余额 | `models.py`, `routes.py` | 对象+区别完整 | 漏 Balance | 泛泛对象 | Movement=当前库存 |
| Q8 | 安全下一步：补 Harness、转移规则、非破坏 smoke/inspect | `routes.py`, `models.py` | 非破坏且具体 | 泛泛测试 | 先改算法/删数据 | 删除 |
| Q9 | 风险：delete route、`check()` 改 Product/Balance、`db.create_all()`、DB 文件 | `routes.py`, `__init__.py` | 写风险完整 | 只说删除 | 无风险 | destructive smoke |

## 独立评分流程

执行 Agent 不看 eval；评分 Agent 只看 eval 和输出。

## 指标提取

重点看 Q5、Q7、Q9 是否准确。只比较本仓库 baseline vs final。

## Harness Design Tradeoff 教师观察点

观察学生是否把 Unit2 理解成“最小可用冷启动地图”，而不是“文档越多越好”。重点看：`AGENTS.md` 是否短入口而非百科全书；`PROJECT_MAP.md` 是否导航核心路径而非复制完整文件树；专题文档是否压缩业务对象、启动、风险和 smoke 路径；新增文档是否让 final Agent 少猜、少误判、少依赖口头补充。

教师还应引导学生区分软约束和硬约束：Unit2 的入口文档、运行手册、风险提示多数只能降低误读，不能强制 Agent 不越界；需要强制执行的边界应留到 Unit3 变成 allowed/forbidden files、permission matrix 或 approval stop。

正式评分应把 Harness 完整度和 Harness 有效度分开：完整度看必要工件是否存在并包含关键部分；有效度看冷启动输出、文件读取路径、误判、不确定表达和 Harness-first routing 是否真的改善。文档过长、过碎或复述源码，只有在证据显示它降低冷启动质量时才作为有效度问题。
## 评分提醒

不要按 Markdown 数量给分。一个清楚的 `TRANSFER_RULES.md` 比一堆空泛文档更有价值。
