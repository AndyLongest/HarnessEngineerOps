# VulpesCRM Unit 4 教师指南

## 1. 仓库特定教学目标

训练学生证明 CRM 查询/筛选 功能不破坏 user/contact/offer 关系，也不误碰 login/signup、删除路由 和 SQLite 数据。

教师观察重点是学生是否能校准完成系统：轻验证暴露什么风险，强完成系统改善什么，哪些验证或交接内容值得保留，哪些只是负担。

## 2. 推荐 Unit4 功能

推荐 `F01 contact search`，可替代为 offer status filter、只读联系人列表筛选、user/contact/offer relationship check。

## 3. 预期的基线过早完成行为

- 只看联系人页面 200；
- 不检查搜索结果是否属于正确 CRM 对象；
- 修改 `database/crm.db` 或模型来让结果匹配；
- 交接 没有 证据路径；
- 忽略 删除路由 和 login/signup 风险。

## 4. 优秀完成门禁应具备的特征

三层 gate 完整，runtime/E2E 能证明登录/用户上下文、联系人或报价筛选结果、CRM 关系一致性。

## 5. 优秀端到端路径应具备的特征

app/测试客户端 + user/contact/offer 数据 + contact search 或 offer filter + 结果集合验证 + 关系完整性验证。

## 6. 优秀交接报告应具备的特征

报告必须写明 功能状态、CRM 关系证据、命令输出、未通过项、清洁状态、下一步安全任务和禁止触碰区域。

## 7. 常见学生错误

- 把 contact search 扩成 CRM 全局重构；
- 只保存截图不保存命令或 response 证据；
- 为了验证方便重置 `database/crm.db`；
- 改 login/signup 或 删除路由；
- 让执行 Agent 自评。

## 8. 教师应在 git diff 中检查什么

- 是否修改 `database/crm.db`；
- 是否改 `models.py`、`db.py`、login/signup；
- 是否改 删除路由；
- 是否只改当前功能允许文件。

## 9. 教师应在验证日志和对比报告中检查什么

- 是否有 user/contact/offer 关系检查；
- 是否有真实输出摘要；
- 路由 200 是否被误用；
- error message 是否能指导 Agent 修复；
- 学生是否说明哪些 gate、E2E、清洁检查或交接内容应保留、放松、合并或删除。

## 10. 建议反馈话术

- “CRM 的完成证据必须覆盖对象关系，不只是页面返回。”
- “contact search 的范围很窄，不应变成登录或数据库重构。”
- “没有 证据路径 的 交接 不能让下一位 Agent 接手。”

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
