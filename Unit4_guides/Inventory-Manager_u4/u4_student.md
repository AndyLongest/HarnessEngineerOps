# Inventory-Manager Unit 4 学生指南

## 目标

Unit 4 要证明一个库存功能真的完成，并且库存状态没有被破坏。本仓库不能只看页面能打开，必须证明产品、库位、移动记录和当前余额一致。

本练习不是要求验证越重越好。你需要比较轻验证收尾和强完成系统，判断哪些验证、E2E、清洁状态和交接内容真正改善了 Agent 能力，哪些只增加负担。

## 1. 选择小功能

优先沿用 Unit3 的同一个 `feature_id`。如果 Unit3 已经选择了下面之外的库存功能，也可以继续使用，但必须保留 Unit3 的 allowed/forbidden files 和验证边界。若课堂需要重新选择，建议只选一个：

- `F01 库存余额只读筛选`
- `F02 产品详情展示验证`
- `F03 小数量转移流程验证`
- `F04 库位库存一致性检查`

## 2. 基线：轻验证完成运行

先不提供完成门禁、E2E 协议、清洁状态检查和 handoff 协议，观察 Agent 如何判断“库存功能是否完成”。

```text
你正在接手 Unit3 的 <feature_id> 库存功能。代码实现已经存在或部分存在，请在不新增 completion gate、E2E 协议、清洁状态检查和 handoff 协议的前提下，判断这个功能是否可以标记为 passing。

请沿用 Unit3 的 feature_list、allowed/forbidden files 和验证信息；不要重新选择功能，不要扩大到 transfer 或 DB 初始化等范围外区域。请记录你运行了哪些检查、为什么认为能或不能 passing、是否更新了 feature_list 证据，并把完整过程保存为 measurement_logs/baseline_completion_run.md。
```

记录它是否只看页面 200，是否跳过余额一致性，是否删除或重置数据。若它判断不能 passing，也要记录它是否能说清缺失证据和下一步安全行动。

基线诊断要围绕四个问题：它是否知道要证明哪个库存行为；它的验证深度是否覆盖库存风险；它是否需要最小 E2E 才能证明余额安全；下一位 Agent 是否能只靠仓库内容接手。

## 3. 构建强完成系统

现在构建一个较完整的完成系统作为对照样本。它不是最终标准答案，而是用来观察更强验证会改善什么，也会带来什么维护和复核负担。

创建：

- `completion_gate.md`
- `completion_gate.json`
- `scripts/verify_<feature_id>.py`
- `verification_logs/<feature_id>_gate_result.md`

强完成系统通常包含三层门禁：

| 层级 | Inventory-Manager 要求 |
|---|---|
| 静态检查 | 检查什么：目标路由、模板和模型引用正确。<br>为什么：先排除明显接线错误。 |
| 运行时检查 | 检查什么：应用或测试客户端能访问目标页面。<br>为什么：证明功能不是只停在代码层面。 |
| 端到端检查 | 只读功能检查什么：目标筛选/详情/库位视图结果正确，且 `Balance`/`Movement` 未改变。transfer 功能检查什么：小数量转移后的库位、移动记录和余额。<br>为什么：证明库存状态保持一致，且没有为验证只读功能而改动库存。 |

任意库存一致性失败，都不能建议通过。

## 4. 最小端到端验证

端到端验证不是单元测试。它必须跑通当前 Unit3 功能对应的一条真实系统路径：启动 Flask 应用或测试客户端，经过 route/template/model，使用真实或最小测试数据，检查页面/响应和数据库状态，并验证库存不变量。

本节不要求覆盖库存系统的所有功能，但必须证明当前功能在系统内真实可运行。只调用 helper、只跑 import、只检查函数返回值、只看页面 200，都不算 E2E。

如果选择的是只读功能，例如 F01/F02/F04：

1. 启动 Flask 应用或创建测试客户端。
2. 准备或确认一个产品、库位和当前余额。
3. 记录查询前的 `Balance`/`Movement` 摘要。
4. 通过目标 route/page 执行筛选、详情页或库位库存查询。
5. 验证页面或响应中的业务结果符合预期。
6. 再次记录 `Balance`/`Movement` 摘要，确认只读操作没有改变库存状态。
7. 确认没有删除产品、库位或重置数据库。

如果选择的是 F03 transfer 功能：

1. 启动 Flask 应用或创建测试客户端。
2. 准备一个产品和两个库位。
3. 通过真实 transfer route 或等价测试客户端流程执行一次小数量转移。
4. 验证来源库位减少、目标库位增加。
5. 验证 `Movement` 记录和 `Balance` 状态一致。
6. 确认库存总量不变，且没有删除产品、库位或重置数据库。

结果保存到 `verification_logs/<feature_id>_e2e_result.md`。报告必须包含入口、数据、步骤、预期业务结果、实际结果、库存不变量和结论。合格证据不是“页面 200”，而是筛选/详情/转移结果与 `Balance`、`Movement`、库存总量之间能互相对上。

如果 E2E 失败，不要把功能标记为 passing。请写 Agent 可读错误消息，说明失败的是查询结果、余额变化、移动记录，还是数据库状态，并指出下一步最小检查动作和禁止触碰区域。

## 5. 清洁状态和交接

完成门禁通过后，还不能立刻宣布完成。当前会话必须留下一个下一位 Agent 可以接手的清洁状态。

`session_exit_checklist.md` 至少覆盖四类检查：

| 类别 | 必须回答 |
|---|---|
| 运行清洁 | Flask 启动、测试客户端或 required tests 是否仍可用？失败时日志在哪里？ |
| 证据清洁 | gate 结果、E2E 结果、feature_list 证据是否指向真实文件？ |
| 工作区清洁 | git diff 是否都在 Unit3 允许范围内？是否有数据库重置、大数量转移、临时 debug 文件或无关修改？ |
| 交接清洁 | 下一步安全任务是什么？哪些库存逻辑、DB 初始化或删除路由禁止触碰？ |

`handoff_report.md` 不能只写“已完成”。它必须写清功能状态、库存一致性证据、命令输出、失败项、清洁状态和下一步安全任务。每个结论都要引用证据路径。

如果任一检查失败，可以结束会话，但不能把功能标记为 passing。保持状态为 `active` 或 `blocked`，并写明失败原因和下一步。

## 6. 交接演练和强完成运行

交接演练的目的不是让新 Agent 继续开发，而是测试仓库内容是否已经足够说明当前状态。新 Agent 只能使用仓库内容和学生保存的工件，不能依赖口头解释。

请让新 Agent 回答：

1. 当前 Unit4 feature 是什么？
2. 它现在是 `passing`、`active` 还是 `blocked`？
3. 完成证据在哪里？
4. E2E 是否真的执行过，库存不变量是否验证过？
5. 当前工作区是否清洁？
6. 下一步最小安全任务是什么？
7. 哪些库存、数据库或删除路径禁止触碰？

把回答保存到 `measurement_logs/next_agent_handoff_drill.md`。合格的交接演练应能找到 feature 状态、gate/E2E/handoff 证据路径，不会把缺证据的功能误判为 passing，并且不需要学生口头补充。

强完成运行不是重新实现功能，而是在已有 completion gate、E2E、清洁状态和 handoff 协议下，再执行一次收尾判断。保存到 `measurement_logs/final_gated_completion_run.md`。

最后写 `unit4_comparison_report.md`，比较轻验证基线和强完成运行：哪些库存完成风险被补上，哪些负担变重，哪些 gate、E2E、清洁检查或交接内容应该保留、放松、合并或删除。最终判断可以比强完成系统更轻，但必须用运行证据解释。

## 7. 交付物

- `measurement_logs/baseline_completion_run.md`
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

## 8. 反误区

页面可访问不等于库存正确；只读功能不能通过执行 transfer 来证明；删除数据不是验证；大数量转移不是冒烟验证；交接必须写清库存状态和证据路径。
