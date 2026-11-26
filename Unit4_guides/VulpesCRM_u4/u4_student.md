# VulpesCRM Unit 4 学生指南

## 目标

Unit 4 要让一个 CRM 功能的完成状态可证明、可复核、可交接。Agent 不能只说联系人搜索或报价筛选已经完成，必须提供用户、联系人、报价关系正确，且注册、登录、删除路由没有被破坏的证据。

本流程仍然以“让完成可证明、可交接”为主。最后对比报告里会有一个简短的 Tradeoff Reflection，用来回看 completion gate、E2E、handoff 和 clean state 检查是刚好够用，还是太轻或太重；这不是新增大任务，只是复盘时做一次设计判断。

## 1. 选择小功能

优先沿用 Unit3 的同一个 `feature_id`。如果 Unit3 已经选择了下面之外的 CRM 功能，也可以继续使用，但必须保留 Unit3 的 allowed/forbidden files 和 CRM 关系边界。若课堂需要重新选择，建议只选一个：

- `F01 联系人搜索`
- `F02 报价状态筛选`
- `F03 只读联系人列表筛选`
- `F04 用户、联系人、报价关系检查`

## 2. 基线完成运行

先不提供完成门禁，观察 Agent 是否过早宣布完成。

```text
你正在接手 Unit3 的 <feature_id> CRM 功能。代码实现已经存在或部分存在，请在不新增 completion gate、E2E 协议、清洁状态检查和 handoff 协议的前提下，判断这个功能是否可以标记为 passing。

请沿用 Unit3 的 feature_list、allowed/forbidden files 和 CRM 关系边界；不要重新选择功能，不要扩大到 login/signup/delete/DB 初始化等范围外区域。请记录你运行了哪些检查、为什么认为能或不能 passing、是否更新了 feature_list 证据，并把完整过程保存为 measurement_logs/baseline_completion_run.md。
```

记录它是否跳过 CRM 关系检查、是否误碰 `database/crm.db`、是否只写“已完成”。若它判断不能 passing，也要记录它是否能说清缺失证据和下一步安全行动。

## 3. 软完成判断运行

在构建 completion gate 之前，先做一轮 soft completion run。只给 Agent 自然语言 checklist，例如“请确认测试、证据、交接都充分”，不要提供 completion gate、gate JSON、E2E 协议、session exit checklist 或 handoff 模板。

VulpesCRM soft completion 常见风险：只证明筛选页面能打开，却没有证明 user/contact/offer 关系一致且 DB/schema 未越界。

请把完整过程保存为 `measurement_logs/soft_completion_run.md`。记录它是否提前 passing、是否漏掉 runtime/E2E、证据路径、清洁状态或交接要求。

## 4. 构建完成门禁

创建：

- `completion_gate.md`
- `completion_gate.json`
- `scripts/verify_<feature_id>.py`
- `verification_logs/<feature_id>_gate_result.md`

门禁至少三层：

| 层级 | VulpesCRM 要求 |
|---|---|
| 静态检查 | 检查什么：目标路由和模板引用正确。<br>为什么：先排除明显接线错误。 |
| 运行时检查 | 检查什么：应用或测试客户端能访问目标页面。<br>为什么：证明功能不是只停在代码层面。 |
| 端到端检查 | 检查什么：准备或确认用户、联系人、报价数据，验证筛选结果。<br>为什么：证明结果只包含正确对象，CRM 关系没有被破坏。 |

任何一层失败，都不能建议通过。

## 5. 最小端到端验证

端到端验证不是单元测试。它必须跑通当前 Unit3 功能对应的一条真实系统路径：启动 Flask 应用或测试客户端，经过 route/template/model，使用真实或最小 CRM 数据，检查页面/响应结果，并验证 user/contact/offer 关系不变量。

本节不要求覆盖 CRM 全流程，但必须证明当前功能在系统内真实可运行。只调用 helper、只跑 import、只检查函数返回值、只看页面 200，都不算 E2E。

1. 启动 Flask 应用或创建测试客户端。
2. 准备或只读确认用户、联系人和报价数据。
3. 通过真实 route/page 执行联系人搜索或报价筛选。
4. 验证页面或响应中的结果只包含正确对象。
5. 验证用户、联系人、报价关系没有被破坏。
6. 确认没有修改 `database/crm.db`、注册登录流程或删除路由。

结果保存到 `verification_logs/<feature_id>_e2e_result.md`。报告必须包含入口、用户或数据记录、步骤、预期 CRM 结果、实际结果、关系不变量和结论。合格证据不是“页面 200”，而是搜索/筛选结果和 user/contact/offer 关系能互相对上。

如果 E2E 失败，不要把功能标记为 passing。请写 Agent 可读错误消息，说明失败的是搜索结果、报价筛选、关系数据，还是 login/signup/delete/SQLite 区域被误碰，并指出下一步最小检查动作和禁止触碰区域。

## 6. 清洁状态和交接

完成门禁通过后，还不能立刻宣布完成。当前会话必须留下一个下一位 Agent 可以接手的清洁状态。

`session_exit_checklist.md` 至少覆盖四类检查：

| 类别 | 必须回答 |
|---|---|
| 运行清洁 | Flask 启动、测试客户端或 required tests 是否仍可用？失败时日志在哪里？ |
| 证据清洁 | gate 结果、CRM E2E 结果、feature_list 证据是否指向真实文件？ |
| 工作区清洁 | git diff 是否都在 Unit3 允许范围内？是否有数据库重置、删除路由调用、调试文件或无关修改？ |
| 交接清洁 | 下一步安全任务是什么？哪些登录、删除和 SQLite 数据区域禁止触碰？ |

`handoff_report.md` 不能只写“已完成”。它必须写清功能状态、证据路径、失败项、清洁状态、下一步安全任务，以及禁止触碰的登录、删除和 SQLite 数据区域。每个结论都要引用证据路径。

如果任一检查失败，可以结束会话，但不能把功能标记为 passing。保持状态为 `active` 或 `blocked`，并写明失败原因和下一步。

## 7. 交接演练和最终运行

交接演练的目的不是让新 Agent 继续开发，而是测试仓库内容是否已经足够说明当前状态。新 Agent 只能使用仓库内容和学生保存的工件，不能依赖口头解释。

请让新 Agent 回答：

1. 当前 Unit4 feature 是什么？
2. 它现在是 `passing`、`active` 还是 `blocked`？
3. 完成证据在哪里？
4. E2E 是否真的执行过，CRM 关系是否验证过？
5. 当前工作区是否清洁？
6. 下一步最小安全任务是什么？
7. 哪些 login/signup/delete/SQLite 区域禁止触碰？

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

页面返回 200 不等于功能完成；Agent 声称完成不等于完成；单元测试通过也不够；必须有最小真实流程、CRM 关系证据、清洁状态和可交接报告。
