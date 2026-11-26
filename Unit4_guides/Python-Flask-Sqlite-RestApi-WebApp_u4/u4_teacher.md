# Python-Flask-Sqlite-RestApi-WebApp Unit 4 教师指南

## 1. 仓库特定教学目标

训练学生在中型 Flask API 仓库中用 scope_contract 控制 完成。目标是验证一个 端点，不是重构 casting agency 全系统。

教师观察重点是学生是否能校准完成系统：轻验证暴露什么风险，强完成系统改善什么，哪些验证或交接内容值得保留，哪些只是负担。

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

## 9. 教师应在验证日志和对比报告中检查什么

- 是否包含 request/响应结构；
- 是否有 DB 状态证据；
- 是否有 out-of-scope un被触碰 检查；
- error message 是否说明 boundary；
- 学生是否说明哪些 gate、E2E、清洁检查或交接内容应保留、放松、合并或删除。

## 10. 建议反馈话术

- “中型仓库的高分来自 scope 清楚，不来自改得多。”
- “路由 200 不是 API 行为验证，响应结构 和 DB 状态要有 证据。”
- “不要让 完成门禁 依赖 admin/setup/mail/upload。”

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
