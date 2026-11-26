# Inventory-Manager Unit 4 教师指南

## 1. 仓库特定教学目标

训练学生把库存 功能的“完成”绑定到库存余额不变量。高分不是多写测试，而是能证明只读筛选/视图 没有破坏 product/location/movement/Balance 关系。

教师观察重点是学生是否能校准完成系统：轻验证暴露什么风险，强完成系统改善什么，哪些验证或交接内容值得保留，哪些只是负担。

## 2. 推荐 Unit4 功能

推荐 `F01 low-stock filter`，也可选 location stock view、movement history 只读视图、transfer 后库存余额检查。

## 3. 预期的基线过早完成行为

- Agent 只看页面能打开就标 passing；
- 只跑 import 或 unit check；
- 不检查 stock balance invariant；
- 把 feature_list 证据留空；
- 跳过 交接 和 清洁状态。

## 4. 优秀完成门禁应具备的特征

三层 gate 必须包含 静态/单元、运行时/集成、端到端/用户流程。Inventory 项目必须额外检查：只读功能不修改 Balance 或 Movement；transfer 功能才执行小数量转移，并验证 location/product balance 和总量不变量。

## 5. 优秀端到端路径应具备的特征

Flask app 或 测试客户端 准备 product/location/balance 数据，执行目标筛选或查询，验证结果和库存余额。只读功能应比较操作前后的 Balance/Movement 摘要，证明没有写入；transfer 功能才需要执行一次小数量转移并验证 Movement。不能只用 路由 200。

## 6. 优秀交接报告应具备的特征

应列出 功能状态、gate/端到端日志、库存 invariant 检查结果、失败过的命令、清洁状态、下一步安全任务和禁止区域。

## 7. 常见学生错误

- 把低库存筛选做成 transfer 重构；
- 为了验证只读筛选而执行或修改 transfer 流程；
- 重置数据库来制造干净数据；
- 没有保存命令输出；
- 只写“库存正常”但没有余额证据；
- 让执行 Agent 自己打分。

## 8. 教师应在 git diff 中检查什么

- 是否修改 transfer logic、models、DB 初始化或 删除路由；
- 是否留下临时 debug 文件；
- 是否只改当前功能允许范围；
- `feature_list.json` 证据 是否指向真实日志。

## 9. 教师应在验证日志和对比报告中检查什么

- 三层 gate 是否都有命令/过程和输出摘要；
- E2E 是否检查 Balance 或库存总量；
- 失败信息是否有 WHAT/WHY/FIX/BOUNDARY；
- 强完成运行是否比基线更可复核；
- 学生是否说明哪些 gate、E2E、清洁检查或交接内容应保留、放松、合并或删除。

## 10. 建议反馈话术

- “路由 200 只能证明页面响应，不能证明库存余额安全。”
- “这个 功能可以很小，但 证据必须能让下一位 Agent 独立判断。”
- “不要为了验证验证低库存筛选而重写 transfer 逻辑。”

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
