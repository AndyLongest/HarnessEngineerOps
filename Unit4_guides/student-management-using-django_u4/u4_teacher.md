# student-management-using-django Unit 4 教师指南

## 1. 仓库特定教学目标

训练学生在大型 Django 仓库中把 完成 绑定到 scope_contract：只做一个角色、一个只读页面、一个最小 E2E，不被 static/vendor、migrations、三角色路由拖走。

## 2. 推荐 Unit4 功能

推荐 `F01 学生成绩只读展示验证`，也可选 student attendance 只读视图、staff attendance 只读流程、HOD single 只读 page filter。

## 3. 预期的基线过早完成行为

- Agent 扫 static/vendor；
- 同时改 HOD/staff/student；
- 运行 migrations、collectstatic；
- 只看页面 200；
- 没有 交接 或 清洁状态。

## 4. 优秀完成门禁应具备的特征

必须包含 scope_contract。三层 gate 只围绕一个角色和一个 view/template，明确未改 static/vendor/migrations，未跨角色。

## 5. 优秀端到端路径应具备的特征

Django 测试客户端 或 runserver，登录/模拟目标角色，访问单一只读页面，验证 attendance/结果/student data display，并检查 scope 未破。

## 6. 优秀交接报告应具备的特征

报告应列出角色、view/template、scope_contract、E2E 证据、禁止区域、清洁状态和 下一步安全任务。

## 7. 常见学生错误

- 允许 `main_app/**` 全目录修改；
- 同时验证三个角色；
- 改 migrations 或 设置；
- 把 UI 全局优化当 Unit4；
- 用文件数和小仓库比较。

## 8. 教师应在 git diff 中检查什么

- 是否改 `main_app/static/**`、migrations、media、设置；
- 是否跨 HOD/staff/student；
- 是否只改 scope_contract 允许文件；
- 是否留下 debug 文件。

## 9. 教师应在验证日志中检查什么

- 是否有角色身份；
- 是否有目标 view/template；
- 是否有只读数据展示 证据；
- 是否有 static/vendor/migrations un被触碰 检查；
- 下一位 Agent 是否无需口头补充。

## 10. 建议反馈话术

- “大 Django 仓库的高分来自 scope 清楚，不来自覆盖全系统。”
- “一个角色一个只读页面已经足够，跨三角色就是本单元要防的风险。”
- “没有 范围证据 的 passing 不可接受。”


## Soft Completion vs Hard Gate 教师观察

Unit4 不重新做三轮开发执行，而是比较完成判断本身。教师重点观察：soft completion 是否过早 passing；hard gate 是否发现 soft run 漏掉的 runtime/E2E、证据路径、清洁状态或交接要求；hard gate 是否因为过重降低复核价值。

课堂结论至少要区分一类可以保留 soft checklist 的完成判断，以及一类必须 hard gate 化的完成证据。
## Harness Design Tradeoff 教师观察点

观察学生是否把 Unit4 理解成“最小可证明的关闭协议”，而不是把 gate、E2E、handoff 做成仪式。重点看：completion gate 是否证明当前功能而非全系统；E2E 是否最小但真实；handoff 是否足够下一位 Agent 接手但不过长；clean-state 检查是否有真实状态证据。

正式评分应把 Harness 完整度和 Harness 有效度分开：完整度看三层 gate、E2E 日志、feature_list 证据、交接和清洁状态是否齐全；有效度看这些证据是否减少提前 passing、证据缺失和口头补充。过重的 gate、E2E 或 handoff 只有在降低清晰度、可执行性或复核价值时才扣分。
## 11. 评分量规

| 评分项 | 分值 |
|---|---:|
| 完成门禁完整度 | 20 |
| 端到端验证质量 | 20 |
| 证据日志质量 | 15 |
| Agent 可读错误消息 | 10 |
| 交接协议质量 | 15 |
| 清洁状态检查 | 10 |
| 基线/最终对比 | 10 |

不按测试数量评分；不按 Markdown 数量评分；不奖励大范围重构；不奖励复杂但不可运行的 E2E；不允许学生只用 Agent 自述作为完成证据。
