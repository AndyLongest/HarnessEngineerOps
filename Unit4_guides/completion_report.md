# Unit 4 指南生成完成报告

## 创建的文件

根目录文件：

- `ClassFile/Unit4_guides/00_overview.md`
- `ClassFile/Unit4_guides/01_unit4_shared_protocol.md`
- `ClassFile/Unit4_guides/02_completion_gate_templates.md`
- `ClassFile/Unit4_guides/03_handoff_templates.md`
- `ClassFile/Unit4_guides/completion_report.md`

每个仓库 创建：

- `student_guide.md`
- `teacher_guide.md`
- `eval.md`

## 每个仓库推荐的 Unit4 功能

| 仓库 | 推荐功能 |
|---|---|
| `Inventory-Manager` | low-stock filter；location stock view；movement history 只读视图；transfer 后库存余额检查 |
| `issue-tracker` | status filter；my assigned tasks；只读搜索；issue detail visibility check |
| `VulpesCRM` | contact search；offer status filter；只读联系人列表筛选；user/contact/offer relationship check |
| `Python-Flask-Sqlite-RestApi-WebApp` | scoped model API 只读筛选；单一 model API 响应验证；单一核心表查询改进；单一端点行为验证 |
| `student-management-using-django` | 单一角色只读页面筛选；一个角色的一条只读流程；attendance/结果 只读视图检查；student 只读数据展示验证 |

## 每个仓库推荐的 E2E 路径

| 仓库 | E2E 路径 |
|---|---|
| `Inventory-Manager` | 只读功能：Flask/测试客户端 + product/location/balance 数据 + 目标查询 + 返回结果 + Balance/Movement 未改变；transfer 功能：小数量转移 + Movement + stock balance invariant |
| `issue-tracker` | 用户/任务准备 + status/assigned/search + 只显示允许访问的问题 + ownership/sharing 边界 |
| `VulpesCRM` | app/测试客户端 + user/contact/offer 数据 + contact/offer filter + CRM 关系检查 |
| `Python-Flask-Sqlite-RestApi-WebApp` | scope_contract + server/测试客户端 + 最小数据 + 目标 API + 响应结构/DB 校验 + admin/setup/mail/upload 未触碰 |
| `student-management-using-django` | scope_contract + 单角色单 view + Django/测试客户端 + 登录/模拟 + 只读显示 + 未改 static/vendor/migrations/跨角色 |

## 老师重点复查的风险

| 仓库 | 复查重点 |
|---|---|
| `Inventory-Manager` | transfer logic、stock balance mutation、DB 初始化、删除路由 |
| `issue-tracker` | Flask-Login、ownership/sharing、update/删除路由、`items.db` |
| `VulpesCRM` | 删除路由、login/signup、CRM 关系、`database/crm.db`、`main.py create_all` |
| `Python-Flask-Sqlite-RestApi-WebApp` | `server.py init_db`、admin/setup/mail/upload、范围漂移、全局重构 |
| `student-management-using-django` | static/vendor、migrations、media/static、email/env 设置、三角色越界 |

## 仍需人工确认

- 教师应确认课堂分组实际使用的 Unit3 功能 ID 与各指南中的建议功能是否一致；若不一致，必须记录功能切换原因，并保证基线和最终仍然比较同一个功能。
- 教师应要求学生记录基线和最终运行的 Agent/模型、时间预算、工具权限和起始代码状态，避免把变量变化误当作 completion gate 的效果。
- 如果学生仓库已有不同文件名的 Harness 工件，应让学生在 handoff_report 中映射真实路径。
- 涉及现有 SQLite 数据或默认账号的验证必须在课堂环境中只读确认。

## 生成约束确认

- 未修改 `UNIT2_GUIDES`。
- 未修改 `UNIT3_GUIDES`。
- 未修改任何业务项目源码、数据库、测试、配置或已有 Harness 文件。
- Unit4 材料聚焦完成门禁、端到端验证、证据日志、Agent 可读错误消息、清洁状态检查、交接协议、下一位 Agent 交接演练 和独立评估。
- Unit4 必须继承 Unit3 的同一功能和范围边界；最终运行只能新增关闭协议能力，不能通过换功能或扩大范围制造改善。
- 没有把 Unit4 写成普通测试课、代码补丁课或总结报告课。
