# student-management-using-django Unit 2 Teacher Guide

## 教师结论

强组仓库。成败在 scope：学生必须让 Agent 路由到 Django 控制面和三角色业务流，而不是陷入 static/vendor。

## 课堂重点

- 规模：约 3688 个 tracked files，大量来自 `main_app/static/`。
- 证据：`README.md`、`manage.py`、`student_management_system/settings.py`、`student_management_system/urls.py`、`main_app/urls.py`、`main_app/models.py`、`views.py`、`hod_views.py`、`staff_views.py`、`student_views.py`、`requirements.txt`。
- 失败点：扫 static/plugins；混淆 HOD 和 Django admin；漏 custom email auth；默认账号不标待确认；建议迁移/collectstatic。

## 候选 Harness 组件

这些是候选组件，不是标准答案：`scope_contract.md`、`AGENTS.md`、`RUNBOOK.md`、`PROJECT_MAP.md`、`DJANGO_ROUTING.md`、`DATA_MODEL.md`、`ROLE_FLOW.md`、`SMOKE_TEST.md`、`KNOWN_RISKS.md`。

学生应先比较 baseline、detailed-doc、final 三次冷启动，再解释最终保留哪些文档以及为什么。

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

## 评分提醒

不要按 Markdown 数量给分。高分是让新 Agent 更少迷路、更能安全接手。教师可从 cold-start trace、eval、对比报告和文档变更中判断学生是否经历了“发现缺口、尝试详细系统、识别成本、再平衡”的过程。
