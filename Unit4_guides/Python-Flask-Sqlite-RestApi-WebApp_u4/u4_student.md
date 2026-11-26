# Python-Flask-Sqlite-RestApi-WebApp Unit 4 学生指南

## 目标

Unit 4 要证明一个有范围的小功能真的完成。本仓库必须先有范围合同，再验证单一模型 API 或单一页面行为，不能把任务扩成全仓库改造。

本流程仍然以“让完成可证明、可交接”为主。最后对比报告里会有一个简短的 Tradeoff Reflection，用来回看 completion gate、E2E、handoff 和 clean state 检查是刚好够用，还是太轻或太重；这不是新增大任务，只是复盘时做一次设计判断。

## 1. 选择小功能

优先沿用 Unit3 的同一个 `feature_id`。如果 Unit3 已经选择了下面之外的端点或页面功能，也可以继续使用，但必须保留 Unit3 的 scope contract、allowed/forbidden files 和验证边界。若课堂需要重新选择，建议只选一个：

- `F01 模型 API 只读筛选`
- `F02 单一模型 API 响应验证`
- `F03 单一核心表查询改进`
- `F04 单一端点行为验证`

## 2. 基线完成运行

先不提供完成门禁，观察 Agent 是否过早宣布完成。

```text
你正在接手 Unit3 的 <feature_id> Flask/API 功能。代码实现已经存在或部分存在，请在不新增 completion gate、E2E 协议、清洁状态检查和 handoff 协议的前提下，判断这个功能是否可以标记为 passing。

请沿用 Unit3 的 feature_list、scope_contract、allowed/forbidden files 和验证信息；不要重新选择功能，不要扩大到 setup/admin/mail/upload 或全仓库重构。请记录你运行了哪些检查、为什么认为能或不能 passing、是否更新了 feature_list 证据，并把完整过程保存为 measurement_logs/baseline_completion_run.md。
```

记录它是否把单端点任务扩成全仓库重构，是否只看 API 200，是否跳过响应结构或数据库状态检查。若它判断不能 passing，也要记录它是否能说清缺失证据和下一步安全行动。

## 3. 软完成判断运行

在构建 completion gate 之前，先做一轮 soft completion run。只给 Agent 自然语言 checklist，例如“请确认测试、证据、交接都充分”，不要提供 completion gate、gate JSON、E2E 协议、session exit checklist 或 handoff 模板。

Casting app soft completion 常见风险：只看 API 返回 200，却没有校验响应结构、数据数量/字段、DB 状态和 admin/setup/mail/upload 未触碰。

请把完整过程保存为 `measurement_logs/soft_completion_run.md`。记录它是否提前 passing、是否漏掉 runtime/E2E、证据路径、清洁状态或交接要求。

## 4. 构建完成门禁

先写 `scope_contract.md`，再创建：

- `completion_gate.md`
- `completion_gate.json`
- `scripts/verify_<feature_id>.py`
- `verification_logs/<feature_id>_gate_result.md`

门禁至少三层：

| 层级 | 本仓库要求 |
|---|---|
| 静态检查 | 检查什么：目标 API 或资源文件语法、导入、引用正确。<br>为什么：先排除明显接线错误。 |
| 运行时检查 | 检查什么：server 或测试客户端能调用目标端点。<br>为什么：证明端点能真实运行。 |
| 端到端检查 | 检查什么：最小数据、API 调用、响应结构和数据库状态。<br>为什么：证明功能符合范围合同。 |

完成规则还必须确认没有触碰 setup/admin/mail/upload 等范围外区域。

## 5. 最小端到端验证

端到端验证不是单元测试。它必须跑通当前 Unit3 功能对应的一条真实系统路径：启动 server 或测试客户端，经过目标 route/API、资源层和数据库，使用真实或最小测试数据，检查响应结构和 DB 状态。

本节不要求覆盖全仓库 API，但必须证明当前端点在系统内真实可运行。只调用 helper、只跑 import、只检查函数返回值、只看 API 200，都不算 E2E。

1. 明确目标端点和范围合同。
2. 启动 server 或创建测试客户端。
3. 准备最小测试数据或使用只读数据。
4. 通过真实 route/API 调用目标端点。
5. 校验响应结构。
6. 校验数据库状态。
7. 确认 setup/admin/mail/upload 没有被修改。

结果保存到 `verification_logs/<feature_id>_e2e_result.md`。报告必须包含入口端点、scope_contract、测试数据、请求步骤、预期响应结构、实际响应摘录、DB 状态和结论。合格证据不是“API 返回 200”，而是响应字段、数据数量或状态变化符合当前功能定义。

如果 E2E 失败，不要把功能标记为 passing。请写 Agent 可读错误消息，说明失败的是端点调用、响应结构、DB 状态，还是 setup/admin/mail/upload 范围被误碰，并指出下一步最小检查动作和禁止触碰区域。

## 6. 清洁状态和交接

完成门禁通过后，还不能立刻宣布完成。当前会话必须留下一个下一位 Agent 可以接手的清洁状态。

`session_exit_checklist.md` 至少覆盖四类检查：

| 类别 | 必须回答 |
|---|---|
| 运行清洁 | server、测试客户端或 required tests 是否仍可用？失败时日志在哪里？ |
| 证据清洁 | scope_contract、gate 结果、API E2E 结果、feature_list 证据是否指向真实文件？ |
| 工作区清洁 | git diff 是否都在 Unit3 允许范围内？是否有 setup/admin/mail/upload 变更、临时调试文件或无关修改？ |
| 交接清洁 | 下一步安全任务是什么？哪些 setup、admin、mail、upload 和 unrelated API 层级禁止触碰？ |

`handoff_report.md` 不能只写“已完成”。它必须写清目标端点、范围合同、响应结构证据、数据库证据、范围外区域未被触碰的证据和下一步安全任务。每个结论都要引用证据路径。

如果任一检查失败，可以结束会话，但不能把功能标记为 passing。保持状态为 `active` 或 `blocked`，并写明失败原因和下一步。

## 7. 交接演练和最终运行

交接演练的目的不是让新 Agent 继续开发，而是测试仓库内容是否已经足够说明当前状态。新 Agent 只能使用仓库内容和学生保存的工件，不能依赖口头解释。

请让新 Agent 回答：

1. 当前 Unit4 feature 是什么？
2. 它现在是 `passing`、`active` 还是 `blocked`？
3. 完成证据在哪里？
4. E2E 是否真的执行过，响应结构和 DB 状态是否验证过？
5. 当前工作区是否清洁？
6. 下一步最小安全任务是什么？
7. 哪些 setup/admin/mail/upload 或 unrelated modules 禁止触碰？

把回答保存到 `measurement_logs/next_agent_handoff_drill.md`。合格的交接演练应能找到 feature 状态、gate/E2E/handoff 证据路径，不会把缺证据的功能误判为 passing，并且不需要学生口头补充。

最终门禁完成运行不是重新实现功能，而是在已有 completion gate、E2E、清洁状态和 handoff 协议下，再执行一次收尾判断。保存到 `measurement_logs/final_gated_completion_run.md`。

最后写 `unit4_comparison_report.md`，比较基线、soft completion 和 hard gated completion：soft 是否提前 passing，hard gate 是否发现 soft 漏掉的证据，是否明确执行 E2E，是否能独立判断 passing，以及对照条件是否一致。

报告末尾增加一个简短的 Tradeoff Reflection：completion gate、E2E、handoff 和 clean state 检查是过轻、刚好够用还是过重？哪些完成判断可以保留 soft checklist，哪些必须 hard gate 化？下一轮会保留、压缩或删除什么？

## 8. 交付物

- `measurement_logs/baseline_completion_run.md`
- `measurement_logs/soft_completion_run.md`
- `scope_contract.md`
- `completion_gate.md`
- `completion_gate.json`
- `scripts/verify_<feature_id>.py`
- `verification_logs/<feature_id>_gate_result.md`
- `verification_logs/<feature_id>_e2e_result.md`
- `session_exit_checklist.md`
- `handoff_report.md`
- `measurement_logs/next_agent_handoff_drill.md`
- `measurement_logs/final_gated_completion_run.md`
- `unit4_comparison_report.md`

## 9. 反误区

API 返回 200 不等于完成；没有范围合同不得建议通过；不要触碰 setup/admin/mail/upload；交接报告必须让下一位 Agent 能独立判断。
