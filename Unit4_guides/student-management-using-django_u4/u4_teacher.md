# student-management-using-django Unit 4 教师指南

## 1. 仓库特定教学目标

训练学生在大型 Django 仓库中把 完成 绑定到 scope_contract：只做一个角色、一个只读页面、一个最小 E2E，不被 static/vendor、migrations、三角色路由拖走。

教师观察重点是学生是否能校准完成系统：轻验证暴露什么风险，强完成系统改善什么，哪些验证或交接内容值得保留，哪些只是负担。

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

## 9. 教师应在验证日志和对比报告中检查什么

- 是否有角色身份；
- 是否有目标 view/template；
- 是否有只读数据展示 证据；
- 是否有 static/vendor/migrations un被触碰 检查；
- 下一位 Agent 是否无需口头补充；
- 学生是否说明哪些 gate、E2E、清洁检查或交接内容应保留、放松、合并或删除。

## 10. 建议反馈话术

- “大 Django 仓库的高分来自 scope 清楚，不来自覆盖全系统。”
- “一个角色一个只读页面已经足够，跨三角色就是本单元要防的风险。”
- “没有 范围证据 的 passing 不可接受。”

## 11. 评分量规

| 评分项 | 分值 |
|---|---:|
| 完成门禁完整度 | 20 |
| 端到端验证质量 | 20 |
| 证据日志质量 | 15 |
| Agent 可读错误消息 | 10 |
| 交接协议质量 | 15 |
| 清洁状态检查 | 10 |
| 校准判断质量 | 10 |

不按测试数量评分；不按 Markdown 数量评分；不奖励大范围重构；不奖励复杂但不可运行的 E2E；不允许学生只用 Agent 自述作为完成证据。最终系统不必最复杂，但必须由基线/强完成运行证据支撑。
