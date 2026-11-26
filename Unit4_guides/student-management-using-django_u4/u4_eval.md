# student-management-using-django Unit 4 评分说明

本文件给独立评分 Agent 使用，不给执行 Agent 使用。

## 1. 目的

评估学生是否在大型 Django 仓库中建立了 scoped 完成协议，并避免 全仓库任务、static/vendor、migrations 和跨角色改动。

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
- Unit3 的 `feature_id`、scope_contract、allowed/forbidden files 和角色边界

## 3. 评估 流程

1. 检查 基线和最终是否比较同一个 Unit3 功能，Agent/工具/时间预算/起始状态差异是否被记录。
2. 检查 基线 是否出现 full-仓库 行为或提前 passing。
3. 检查 scope_contract 是否存在且具体到一个角色/一个 view。
4. 检查 完成门禁 三层是否完整。
5. 检查 E2E 是否验证只读 attendance/结果/student data display。
6. 对照 diff 检查 static/vendor/migrations/设置/跨角色。
7. 检查 交接是否让下一位 Agent 独立接手。
8. 比较 最终 是否比 基线 更可证明、更可交接。

## 4. 指标

- scope_contract 具体程度；
- full-仓库 行为次数；
- 跨角色 变更；
- static/vendor/migrations 被触碰；
- 端到端只读证据；
- 基线/最终对照条件是否一致；
- 交接所需口头补充次数；
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
- Django 特有红旗：修改 static/vendor、migrations、设置，或同时改 HOD/staff/student 三个角色。

## 7. 输出格式

```markdown
# Unit 4 独立评估: student-management-using-django

## 分数
- 总分: __ / 100

## 发现
- scope_contract:
- 完成门禁:
- Django 端到端验证:
- 只读数据证据:
- Static/vendor/migrations un被触碰:
- 交接:
- 清洁状态:
- 基线 vs 最终:

## 红旗问题
-

## 最终判断
通过 / 需要修改
```
