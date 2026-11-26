# Unit 4 总览：可证明、可复核、可交接的完成协议

## Unit4 总目标

Unit4 的核心目标是：

> 让“完成”从 Agent 的主观声明，变成一套可执行、可复核、可交接的关闭协议。

学生要训练的不是“多写测试”或“多写总结”，而是让一个功能的完成状态必须经过 完成门禁、端到端验证、证据日志、清洁状态检查、交接协议、下一位 Agent 交接演练 和独立评估。

## Unit2 / Unit3 / Unit4 的区别

| Unit | 训练问题 | 核心证据 |
|---|---|---|
| Unit2 | 新 Agent 能不能冷启动、看懂仓库、找到安全下一步 | 基线/最终 冷启动、Harness 路由质量、口头补充次数 |
| Unit3 | Agent 能不能在边界内执行，遵守 WIP=1 和 sprint contract | feature_list、permission matrix、task trace、overreach 是否减少 |
| Unit4 | Agent 说完成之后，是否真的完成，是否可交接 | 完成门禁、E2E 证据、清洁状态、交接演练、独立评分 |

基线和最终只能在同一仓库、同一 Unit3 功能内比较。不同仓库之间不比较耗时、文件数或复杂度。

## Unit4 实验控制

Unit4 不是重新选择一个新需求，而是接住 Unit3 已经进入 `active` 或已完成实现但尚未完成关闭协议的同一个功能。学生必须沿用 Unit3 的 `feature_id`、行为描述、allowed/forbidden files、验证命令和证据字段；如果课堂需要更换功能，必须在 `unit4_comparison_report.md` 中说明原因，并且基线和最终仍然使用同一个新功能。

Unit4 延续 Unit3 的软/硬约束对比，但只聚焦完成判断。软完成运行使用自然语言 checklist 判断是否可以 passing；硬完成运行使用 completion gate、E2E evidence、handoff drill 和 session exit checklist 判断是否可以 passing。

为了让基线/最终对比有效，学生需要在两次运行中保持以下条件一致或记录差异：

- 同一个仓库、同一个功能、同一套起始代码状态，或保存可复核的起始 diff。
- 同一个 Agent/模型类型、相近时间预算和相同工具权限。
- 同一份 Unit3 范围边界，最终运行只能新增 completion gate、E2E、清洁状态和 handoff 协议。
- 不把最终运行的改善归因于更换功能、扩大范围或人工口头补充。

## Unit4_guides 目录结构

```text
ClassFile/Unit4_guides/
├── 00_overview.md
├── 01_unit4_shared_protocol.md
├── 02_completion_gate_templates.md
├── 03_handoff_templates.md
├── completion_report.md
├── Inventory-Manager/
│   ├── student_guide.md
│   ├── teacher_guide.md
│   └── eval.md
├── issue-tracker/
│   ├── student_guide.md
│   ├── teacher_guide.md
│   └── eval.md
├── VulpesCRM/
│   ├── student_guide.md
│   ├── teacher_guide.md
│   └── eval.md
├── Python-Flask-Sqlite-RestApi-WebApp/
│   ├── student_guide.md
│   ├── teacher_guide.md
│   └── eval.md
└── student-management-using-django/
    ├── student_guide.md
    ├── teacher_guide.md
    └── eval.md
```

## 五个仓库的推荐功能

| 仓库 | 推荐 Unit4 功能|
|---|---|
| `Inventory-Manager` | low-stock filter；location stock view；movement history 只读视图；transfer 后库存余额检查 |
| `issue-tracker` | status filter；my assigned tasks；只读搜索；issue detail visibility check |
| `VulpesCRM` | contact search；offer status filter；只读联系人列表筛选；user/contact/offer relationship check |
| `Python-Flask-Sqlite-RestApi-WebApp` | scoped model API 只读筛选；单一 model API 响应验证；单一核心表查询改进；单一端点行为验证 |
| `student-management-using-django` | 单一角色只读页面筛选；一个 HOD/staff/student 只读流程；attendance/结果 只读视图检查；student 只读数据展示验证 |

## 五个仓库的 E2E 路径

| 仓库 | 推荐最小 E2E 路径 |
|---|---|
| `Inventory-Manager` | 只读功能：启动 Flask 或 测试客户端；准备 product/location/balance 数据；执行筛选或查询；验证结果；确认 Balance/Movement 未改变。transfer 功能：执行一次小数量转移；验证来源/目标余额、Movement 记录和总量不变量。 |
| `issue-tracker` | 准备或模拟用户；读取 issue/task；执行 status/assigned/search；确认 只显示允许访问的问题；验证 ownership/sharing 未破坏 |
| `VulpesCRM` | 启动 app 或 测试客户端；准备 user/contact/offer；执行 contact search 或 offer filter；验证结果；验证 CRM 关系未破坏 |
| `Python-Flask-Sqlite-RestApi-WebApp` | 明确 scope_contract；启动 server 或 测试客户端；初始化最小数据；调用目标 API；校验 响应结构 和 DB 状态；确认 admin/setup/mail/upload 未被触碰 |
| `student-management-using-django` | 先写 scope_contract；只选一个角色和一个 view；启动 Django 或 测试客户端；登录/模拟目标角色；访问页面；校验只读数据；确认未改 static/vendor/migrations 且未跨角色 |

## 五个仓库的高风险区域

| 仓库 | 高风险区域 |
|---|---|
| `Inventory-Manager` | transfer logic、stock balance mutation、数据库初始化、破坏性删除路由 |
| `issue-tracker` | Flask-Login、ownership、sharing 权限、update/删除路由、数据库初始化、`items.db` |
| `VulpesCRM` | 删除路由、login/signup、offer/contact/user flow、`database/crm.db`、`main.py` 启动 建表 |
| `Python-Flask-Sqlite-RestApi-WebApp` | `server.py init_db`、setup/admin 路径、mail/upload 配置、多个 model/API 层级、中型仓库范围漂移 |
| `student-management-using-django` | static/vendor、migrations、media/static 输出、email/env 设置、destructive delete views、three-role 路由 |

## 教师使用方式

给每组学生只发对应仓库的 `student_guide.md`。教师使用对应 `teacher_guide.md` 观察课堂表现、复查 git diff 和 验证日志。独立评分 Agent 只在学生产出完成后使用 `eval.md`，不得把 `eval.md` 交给执行 Agent。

评分不按测试数量、Markdown 数量或重构规模。评分看 完成门禁 是否完整、E2E 是否能证明最小真实路径、证据 是否可复核、交接是否能让下一位 Agent 无口头补充接手。

## 学生分发规则

每个学生组只拿一个项目包的 `student_guide.md` 和共享模板文件。不要给学生其他仓库的评分细则，也不要让执行 Agent 自己读取 `eval.md` 后自评。

## Harness Design Tradeoff Reminder

Unit4 仍然要求学生建立最小可证明的关闭协议，不是把完成门禁做成沉重仪式。完成证据要足够独立复核，但验证负担必须和功能风险匹配。

Soft completion 和 hard gated completion 的区别必须清楚：soft completion 依赖 Agent 自觉检查测试、证据和交接是否充分；hard gated completion 要求证据文件、三层 gate、E2E、清洁状态和交接演练都能被独立复核。

学生应在最终对比中轻量反思四个取舍：

- 验证太轻 vs 验证太重。
- E2E 缺失 vs E2E 过度。
- handoff 太短 vs handoff 太长。
- clean state 缺失 vs 退出检查仪式化。

正式设计评价主要放在 teacher guide 和 eval 中：看完成门禁是否提高可证明性和可交接性，同时没有制造无法运行、无人阅读或不能维护的负担。
