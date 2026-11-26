# issue-tracker Unit 4 教师指南

## 1. 仓库特定教学目标

训练学生证明 issue/task 功能不破坏权限边界。核心不是 status filter 是否好看，而是 Flask-Login、ownership、sharing、update/删除路由 在收尾时仍可复核。

教师观察重点是学生是否能校准完成系统：轻验证暴露什么风险，强完成系统改善什么，哪些验证或交接内容值得保留，哪些只是负担。

## 2. 推荐 Unit4 功能

推荐 `F01 status filter`，可替代为 my assigned tasks、只读搜索、issue detail visibility check。

## 3. 预期的基线过早完成行为

- 只证明 filter 返回 200；
- 没有模拟第二个用户；
- 忽略 shared task 和 private task；
- feature_list 证据为空；
- 交接 只写“已完成”。

## 4. 优秀完成门禁应具备的特征

三层 gate 都有 证据，且 runtime/E2E 必须覆盖 owner、shared user、unauthorized user 至少两个权限状态。

## 5. 优秀端到端路径应具备的特征

准备用户和任务，执行目标筛选/详情访问，验证 只显示允许访问的问题，并确认 删除/更新路由 未被改坏。

## 6. 优秀交接报告应具备的特征

应列出权限场景、用户身份、命令或 测试客户端 输出、功能状态、失败项、下一步安全任务和禁止触碰区域。

## 7. 常见学生错误

- 把权限验证写成“登录后能访问页面”；
- 为了测试方便重置 `items.db`；
- 只检查 owner，不检查 shared/unauthorized；
- 改 update/删除路由 来绕过问题；
- 让执行 Agent 自己评分。

## 8. 教师应在 git diff 中检查什么

- 是否修改 Flask-Login/auth；
- 是否误改 ownership/sharing helpers；
- 是否改 删除/更新路由；
- 是否修改或重置 `items.db`；
- 是否留下 debug 文件。

## 9. 教师应在验证日志和对比报告中检查什么

- 是否有 user/permission 场景；
- 是否有命令输出或 response excerpt；
- 路由 200 是否被误当业务完成；
- failure message 是否包含 WHAT/WHY/FIX/BOUNDARY；
- 学生是否说明哪些 gate、E2E、清洁检查或交接内容应保留、放松、合并或删除。

## 10. 建议反馈话术

- “issue-tracker 的完成证据必须包含权限边界，不只是列表能显示。”
- “只读搜索 如果泄漏 private issue，就不能 passing。”
- “不要通过改 删除/更新路由 来让 E2E 变绿。”

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
