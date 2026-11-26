# Python-Flask-Sqlite-RestApi-WebApp Unit 4 教师指南

## 1. 仓库特定教学目标

训练学生在中型 Flask API 仓库中用 scope_contract 控制 完成。目标是验证一个 端点，不是重构 casting agency 全系统。

## 2. 推荐 Unit4 功能

推荐 `F01 scoped model API 只读筛选`，也可选 单一 model API 响应验证、单一核心表查询改进、单一端点行为验证。

## 3. 预期的基线过早完成行为

- Agent 顺手读改 admin/setup/mail/upload；
- 路由 200 被当成完成；
- 响应结构 没验证；
- DB 状态没检查；
- 全局重构 unrelated modules。

## 4. 优秀完成门禁应具备的特征

gate 必须包含 scope_contract，三层证据必须只围绕目标 端点，并声明哪些目录/配置未被触碰。

## 5. 优秀端到端路径应具备的特征

server/测试客户端 + 最小数据 + 目标 API call + 响应结构 + DB 状态 + admin/setup/mail/upload un被触碰。

## 6. 优秀交接报告应具备的特征

应写出目标 端点、scope、命令、response excerpt、DB check、禁止触碰区域和 下一步安全任务。

## 7. 常见学生错误

- 把单 端点 做成全仓库 清洁up；
- 修改 `server.py init_db` 或 设置；
- 不验证 响应结构；
- 没有说明 admin/setup/mail/upload 是否 un被触碰；
- 把复杂但不可运行的 E2E 当高分。

## 8. 教师应在 git diff 中检查什么

- 是否改 admin/setup/mail/upload；
- 是否改不在 scope 的 models/路由/templates；
- 是否修改 `.idea`、DevOps 或无关静态文件；
- scope_contract 是否和实际 diff 一致。

## 9. 教师应在验证日志中检查什么

- 是否包含 request/响应结构；
- 是否有 DB 状态证据；
- 是否有 out-of-scope un被触碰 检查；
- error message 是否说明 boundary。

## 10. 建议反馈话术

- “中型仓库的高分来自 scope 清楚，不来自改得多。”
- “路由 200 不是 API 行为验证，响应结构 和 DB 状态要有 证据。”
- “不要让 完成门禁 依赖 admin/setup/mail/upload。”


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
