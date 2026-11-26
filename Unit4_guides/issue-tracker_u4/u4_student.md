# issue-tracker Unit 4 学生指南

## 目标

Unit 4 要让一个问题追踪功能的完成状态可证明、可复核、可交接。本仓库必须证明权限边界正确：owner、shared user、未授权用户的可见性不能混淆。

本流程仍然以“让完成可证明、可交接”为主。最后对比报告里会有一个简短的 Tradeoff Reflection，用来回看 completion gate、E2E、handoff 和 clean state 检查是刚好够用，还是太轻或太重；这不是新增大任务，只是复盘时做一次设计判断。

## 1. 选择小功能

优先沿用 Unit3 的同一个 `feature_id`。如果 Unit3 已经选择了下面之外的 issue-tracker 功能，也可以继续使用，但必须保留 Unit3 的 allowed/forbidden files 和权限边界。若课堂需要重新选择，建议只选一个：

- `F01 状态筛选`
- `F02 我的指派任务`
- `F03 只读搜索`
- `F04 问题详情可见性检查`

## 2. 基线完成运行

先不提供完成门禁，观察 Agent 是否过早宣布完成。

```text
你正在接手 Unit3 的 <feature_id> issue-tracker 功能。代码实现已经存在或部分存在，请在不新增 completion gate、E2E 协议、清洁状态检查和 handoff 协议的前提下，判断这个功能是否可以标记为 passing。

请沿用 Unit3 的 feature_list、allowed/forbidden files 和权限边界；不要重新选择功能，不要扩大到 update/delete/DB 初始化等范围外区域。请记录你运行了哪些检查、为什么认为能或不能 passing、是否更新了 feature_list 证据，并把完整过程保存为 measurement_logs/baseline_completion_run.md。
```

记录它是否只看路由 200，是否忽略未授权用户，是否没有权限证据就标记完成。若它判断不能 passing，也要记录它是否能说清缺失证据和下一步安全行动。

## 3. 软完成判断运行

在构建 completion gate 之前，先做一轮 soft completion run。只给 Agent 自然语言 checklist，例如“请确认测试、证据、交接都充分”，不要提供 completion gate、gate JSON、E2E 协议、session exit checklist 或 handoff 模板。

issue-tracker soft completion 常见风险：只验证登录用户能看到页面，却没有证明 owner/shared/unauthorized visibility 没有泄漏。

请把完整过程保存为 `measurement_logs/soft_completion_run.md`。记录它是否提前 passing、是否漏掉 runtime/E2E、证据路径、清洁状态或交接要求。

## 4. 构建完成门禁

创建：

- `completion_gate.md`
- `completion_gate.json`
- `scripts/verify_<feature_id>.py`
- `verification_logs/<feature_id>_gate_result.md`

门禁至少三层：

| 层级 | issue-tracker 要求 |
|---|---|
| 静态检查 | 检查什么：目标路由、辅助函数和模板引用正确。<br>为什么：先排除明显接线错误。 |
| 运行时检查 | 检查什么：应用或测试客户端能登录用户并访问目标页面或 API。<br>为什么：证明功能能在登录状态下运行。 |
| 端到端检查 | 检查什么：用户 A、用户 B 的任务可见性。<br>为什么：证明 owner/shared user 权限没有被破坏。 |

任意权限边界失败，都不能建议通过。

## 5. 最小端到端验证

端到端验证不是单元测试。它必须跑通当前 Unit3 功能对应的一条真实系统路径：启动 Flask 应用或测试客户端，经过登录/session、route/template 或 API，使用真实或最小测试数据，检查页面/响应结果，并验证权限不变量。

本节不要求覆盖整个权限系统，但必须证明当前功能在系统内真实可运行。只调用 query/helper、只跑 import、只检查函数返回值、只看路由 200，都不算 E2E。

1. 启动 Flask 应用或创建测试客户端。
2. 准备或模拟两个用户，并建立登录/session 状态。
3. 创建一个私有任务和一个共享任务。
4. 通过真实 route/page/API 执行状态筛选、指派视图、只读搜索或详情访问。
5. 验证页面或响应中用户只能看到自己拥有或被共享的问题。
6. 确认更新和删除路由没有被误改。

结果保存到 `verification_logs/<feature_id>_e2e_result.md`。报告必须包含入口、用户身份、测试数据、步骤、预期可见性、实际结果、权限不变量和结论。合格证据不是“路由 200”，而是 owner、shared user、未授权用户的返回结果能证明没有泄漏 private issue。

如果 E2E 失败，不要把功能标记为 passing。请写 Agent 可读错误消息，说明失败的是 owner 可见性、shared 可见性、未授权访问，还是 update/delete 路由被误碰，并指出下一步最小检查动作和禁止触碰区域。

## 6. 清洁状态和交接

完成门禁通过后，还不能立刻宣布完成。当前会话必须留下一个下一位 Agent 可以接手的清洁状态。

`session_exit_checklist.md` 至少覆盖四类检查：

| 类别 | 必须回答 |
|---|---|
| 运行清洁 | Flask 启动、登录路径、测试客户端或 required tests 是否仍可用？失败时日志在哪里？ |
| 证据清洁 | gate 结果、权限 E2E 结果、feature_list 证据是否指向真实文件？ |
| 工作区清洁 | git diff 是否都在 Unit3 允许范围内？是否有 `items.db` 重置、调试文件或无关修改？ |
| 交接清洁 | 下一步安全任务是什么？哪些 auth、update/delete、DB 初始化路径禁止触碰？ |

`handoff_report.md` 不能只写“已完成”。它必须写清用户和权限场景、证据路径、禁止触碰的路由、当前清洁状态和下一步安全任务。每个结论都要引用证据路径。

如果任一检查失败，可以结束会话，但不能把功能标记为 passing。保持状态为 `active` 或 `blocked`，并写明失败原因和下一步。

## 7. 交接演练和最终运行

交接演练的目的不是让新 Agent 继续开发，而是测试仓库内容是否已经足够说明当前状态。新 Agent 只能使用仓库内容和学生保存的工件，不能依赖口头解释。

请让新 Agent 回答：

1. 当前 Unit4 feature 是什么？
2. 它现在是 `passing`、`active` 还是 `blocked`？
3. 完成证据在哪里？
4. E2E 是否真的执行过，权限边界是否验证过？
5. 当前工作区是否清洁？
6. 下一步最小安全任务是什么？
7. 哪些 auth、DB、update/delete 路径禁止触碰？

把回答保存到 `measurement_logs/next_agent_handoff_drill.md`。合格的交接演练应能找到 feature 状态、gate/E2E/handoff 证据路径，不会把缺证据的功能误判为 passing，并且不需要学生口头补充。

最终门禁完成运行不是重新实现功能，而是在已有 completion gate、E2E、清洁状态和 handoff 协议下，再执行一次收尾判断。保存到 `measurement_logs/final_gated_completion_run.md`。

最后写 `unit4_comparison_report.md`，比较基线、soft completion 和 hard gated completion：soft 是否提前 passing，hard gate 是否发现 soft 漏掉的证据，是否明确执行 E2E，是否能独立判断 passing，以及对照条件是否一致。

报告末尾增加一个简短的 Tradeoff Reflection：completion gate、E2E、handoff 和 clean state 检查是过轻、刚好够用还是过重？哪些完成判断可以保留 soft checklist，哪些必须 hard gate 化？下一轮会保留、压缩或删除什么？

## 8. 交付物

- `measurement_logs/baseline_completion_run.md`
- `measurement_logs/soft_completion_run.md`
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

列表返回数据不等于权限正确；路由 200 不等于完成；不要重置 `items.db`；不要把交接报告写成流水账，必须让下一位 Agent 能独立判断。
