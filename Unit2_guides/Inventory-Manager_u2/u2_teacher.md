# Inventory-Manager Unit 2 Teacher Guide

## 教师结论

适合弱组。仓库小，但库存转移规则能清楚展示 Harness 的价值：让 Agent 少猜业务状态变化。

## 课堂重点

- 规模：约 12 个 tracked files，全仓库 Unit 2。
- 证据：`README.md`、`run.py`、`flaskinventory/__init__.py`、`routes.py`、`models.py`、`forms.py`、`requirements.txt`。
- 失败点：编造登录；漏 `Balance`；忽略 `db.create_all()`；不理解转移会写库存。

## 候选 Harness 组件

这些是候选组件，不是标准答案：`AGENTS.md`、`RUNBOOK.md`、`PROJECT_MAP.md`、`DATA_MODEL.md`、`TRANSFER_RULES.md`、`SMOKE_TEST.md`、`KNOWN_RISKS.md`。

学生应先比较 baseline、detailed-doc、final 三次冷启动，再解释最终保留哪些文档以及为什么。

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

重点看 Q5、Q7、Q9 是否准确。只比较本仓库 baseline、detailed-doc 和 final。

## 评分提醒

不要按 Markdown 数量给分。一个清楚的 `TRANSFER_RULES.md` 比一堆空泛文档更有价值。教师可从 cold-start trace、eval、对比报告和文档变更中判断学生是否经历了“发现缺口、尝试详细系统、识别成本、再平衡”的过程。
