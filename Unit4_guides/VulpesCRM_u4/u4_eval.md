# VulpesCRM Unit 4 评分说明

本文件给独立评分 Agent 使用，不给执行 Agent 使用。

## 1. 目的

评估学生是否为 VulpesCRM 的 contact/offer 功能建立了可复核关闭协议，并证明 user/contact/offer 关系未被破坏。

## 2. 必需输入

- `measurement_logs/baseline_completion_run.md`
- `measurement_logs/soft_completion_run.md`
- `measurement_logs/final_gated_completion_run.md`
- `measurement_logs/next_agent_handoff_drill.md`
- `completion_gate.md`
- `completion_gate.json`
- `verification_logs/<feature_id>_gate_result.md`
- `verification_logs/<feature_id>_e2e_result.md`
- `session_exit_checklist.md`
- `handoff_report.md`
- `feature_list.json`
- git diff 摘要
- `unit4_comparison_report.md`
- Unit3 的 `feature_id`、allowed/forbidden files 和 CRM 关系边界

## 3. 评估 流程

1. 检查 基线和最终是否比较同一个 Unit3 功能，Agent/工具/时间预算/起始状态差异是否被记录。
2. 检查 基线 的提前完成声明。
3. 检查 gate 是否三层完整。
4. 检查 E2E 是否验证 user/contact/offer 关系。
5. 检查 diff 是否触碰 DB、login/signup、删除路由、核心模型关系。
7. 检查 清洁状态和交接是否独立可读。
8. 比较 hard gated completion 是否比 基线 更可验证和可交接。

## 4. 指标

- soft completion 提前 passing；
- 过早完成声明；
- 缺失证据项；
- CRM relationship 证据；
- DB/delete/login out-of-scope 变更；
- 基线/最终对照条件是否一致；
- 下一位 Agent oral supplement count；
- 清洁状态完整度。

## Harness Design Scoring Lens

Score Harness completeness and Harness effectiveness separately.

- Completeness: completion gate, gate JSON, verification logs, E2E result, feature_list evidence, session exit checklist, handoff report, and handoff drill are present and internally consistent.
- Effectiveness: soft completion exposes premature passing risk; hard/final run reduces premature passing, missing evidence, oral supplementation, and ambiguity about whether the feature is `passing`; the next Agent can replay the evidence without teacher explanation.
- Soft vs hard scoring: soft checklist is acceptable for low-risk reminders, but completion evidence that blocks passing should be hard-gated and independently reviewable.
- Tradeoff / overdesign signals: verification too light, verification too heavy, missing E2E, excessive E2E, handoff too short, handoff too long, missing clean state, or ritualized clean state. Penalize over-heavy artifacts only when they reduce clarity, executability, or independent review value.
- Advanced reflection, not hard scoring unless evidenced: long-term maintenance burden, future pruning, and alternate balanced gate designs.

## 5. 评分量规

| 评分项 | 分值 |
|---|---:|
| 完成门禁完整度 | 20 |
| 端到端验证质量 | 20 |
| 证据日志质量 | 15 |
| Agent 可读错误消息 | 10 |
| 交接协议质量 | 15 |
| 清洁状态检查 | 10 |
| soft/hard 完成对比 | 10 |

## 6. 红旗问题

- 只有 Agent 自述，没有命令输出；
- 只有单元测试，没有 runtime / E2E；
- 功能被标记 passing，但 证据为空；
- 路由 200 被当作业务完成；
- handoff_report 只写“已完成”，没有证据路径；
- 下一位 Agent 无法判断当前状态；
- 修改了 out-of-scope 文件；
- 对 Django 大仓库做 全仓库任务；
- 对中型 Flask 项目无 scope 地全局重构；
- 删除或重置数据库；
- 把临时 debug 文件留在仓库；
- VulpesCRM 特有红旗：误改 login/signup、删除路由、`database/crm.db` 或 user/contact/offer 关系。

## 7. 输出格式

```markdown
# Unit 4 独立评估: VulpesCRM

## 分数
- 总分: __ / 100

## 发现
- 完成门禁:
- CRM E2E:
- Relationship 证据:
- 证据日志:
- Error messages:
- 交接:
- 清洁状态:
- 基线 vs 最终:

## 红旗问题
-

## 最终判断
通过 / 需要修改
```
