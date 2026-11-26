# student-management-using-django Unit 2 Teacher Guide

## 教师结论

强组仓库。成败在 scope：学生必须让 Agent 路由到 Django 控制面和三角色业务流，而不是陷入 static/vendor。

## 课堂重点

- 规模：约 3688 个 tracked files，大量来自 `main_app/static/`。
- 证据：`README.md`、`manage.py`、`student_management_system/settings.py`、`student_management_system/urls.py`、`main_app/urls.py`、`main_app/models.py`、`views.py`、`hod_views.py`、`staff_views.py`、`student_views.py`、`requirements.txt`。
- 失败点：扫 static/plugins；混淆 HOD 和 Django admin；漏 custom email auth；默认账号不标待确认；建议迁移/collectstatic。

## 推荐学生新增工件

`scope_contract.md`、`AGENTS.md`、`RUNBOOK.md`、`PROJECT_MAP.md`、`DJANGO_ROUTING.md`、`DATA_MODEL.md`、`ROLE_FLOW.md`、`SMOKE_TEST.md`、`KNOWN_RISKS.md`。

## Eval：标准答案和评分规则

| Q | 标准答案 | 证据路径 | 满分 | 半分 | 零分 | 常见错答 |
|---|---|---|---|---|---|---|
| Q1 | Django 学生管理系统，HOD/admin、staff、student 三角色，课程/科目/考勤/成绩/请假/反馈/通知 | `README.md`, `main_app/urls.py`, `models.py` | 角色+业务完整 | generic school app | 领域错 | static site |
| Q2 | Django 3.1.1, SQLite default + dj-database-url override, custom user/email auth, Whitenoise, Pillow, gunicorn | `requirements.txt`, `settings.py`, `EmailBackend.py` | 栈完整 | Django/SQLite only | Flask/Node | 漏 custom user |
| Q3 | `pip3 install -r requirements.txt`，建议 virtualenv | `README.md`, `requirements.txt` | 命令+venv | 只有安装 | 错命令 | npm |
| Q4 | `python manage.py runserver`；settings 为 `student_management_system.settings`；urls include `main_app.urls` | `README.md`, `manage.py`, `urls.py` | 命令+路由 | 只有命令 | 错入口 | app.py |
| Q5 | root login 和 `doLogin/`；README 默认 HOD/staff/student 账号需 DB 确认；可 createsuperuser | `README.md`, `main_app/urls.py`, `views.py` | 路由+账号 caveat | 只说默认账号 | 编造 signup | 无认证 |
| Q6 | 默认 SQLite `db.sqlite3`，dj_database_url 可覆盖；migrations 存在；初始用户依赖 DB/createsuperuser，待确认 | `settings.py`, `README.md`, `migrations` | DB+override+未知边界 | SQLite only | seed guaranteed | 外部 only |
| Q7 | `CustomUser`, `Admin`, `Staff`, `Student`, `Course`, `Subject`, `Session`, `Attendance`, `AttendanceReport`, leave/feedback/notification, `StudentResult` | `main_app/models.py` | 核心模型完整 | 漏部分 | 泛泛 users/courses | 漏 attendance/result |
| Q8 | 安全下一步：补 scoped Harness、role-flow map、routing map、只读 smoke；避免 migrations/collectstatic/deletes/DB writes | `urls.py`, `settings.py`, `models.py` | scoped 非破坏 | 泛泛 docs | 运行破坏命令 | 解释 static 全树 |
| Q9 | 风险：`db.sqlite3`、migrations、media/static、`STATIC_ROOT`、email env、secret/ALLOWED_HOSTS/debug、删除路由、auth/password | `settings.py`, `main_app/urls.py`, `hod_views.py` | 风险完整 | 只说 debug | 无风险 | 运行删除/迁移 |

## 独立评分流程

执行 Agent 不看 eval；评分 Agent 只看 eval 和输出。不要因学生没解释全部 static/vendor 扣分。

## 指标提取

除了常规指标，记录是否遵守大仓库 scope。文件数不一定下降，第一批文件必须更合理。

## Harness Design Tradeoff 教师观察点

观察学生是否把 Unit2 理解成“最小可用冷启动地图”，而不是“文档越多越好”。重点看：`AGENTS.md` 是否短入口而非百科全书；`PROJECT_MAP.md` 是否导航核心路径而非复制完整文件树；专题文档是否压缩业务对象、启动、风险和 smoke 路径；新增文档是否让 final Agent 少猜、少误判、少依赖口头补充。

教师还应引导学生区分软约束和硬约束：Unit2 的入口文档、运行手册、风险提示多数只能降低误读，不能强制 Agent 不越界；需要强制执行的边界应留到 Unit3 变成 allowed/forbidden files、permission matrix 或 approval stop。

正式评分应把 Harness 完整度和 Harness 有效度分开：完整度看必要工件是否存在并包含关键部分；有效度看冷启动输出、文件读取路径、误判、不确定表达和 Harness-first routing 是否真的改善。文档过长、过碎或复述源码，只有在证据显示它降低冷启动质量时才作为有效度问题。
## 评分提醒

不要按 Markdown 数量给分。高分是让新 Agent 更少迷路、更能安全接手。
