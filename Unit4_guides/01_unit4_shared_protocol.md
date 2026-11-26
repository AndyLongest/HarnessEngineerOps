# Unit 4 新仓库学生教材生成协议

## 0. 用途

本文件是一份自包含的 Unit 4 教材生成协议。生成 Agent 只需要本文件、一个目标仓库和一句简单提示词，就应能够生成：

`Unit4_guides/<repo-name>_u4/u4_student.md`

不要假设 Agent 可以读取其他 protocol、completion template、handoff template、示例教材、teacher guide 或 eval。只生成学生指南，不生成评分答案，不修改目标项目源码。

推荐提示词：

```text
请严格按照《Unit 4 新仓库学生教材生成协议》，分析 <目标仓库路径>，生成该仓库的 u4_student.md。只生成学生指南，不修改项目源码；完成后执行协议中的自检。
```

## 1. 生成边界与仓库分析

必须阅读实际仓库，确认：核心用户流程、角色/权限、状态写入、测试和启动入口、数据库/上传/外部服务、已有 Unit 3 工件、高风险区域和可执行的最小验证路径。

生成过程只读。除目标 `u4_student.md` 外，不修改源码、数据库、依赖、配置、迁移或现有 Harness。路径和命令必须有仓库证据；无法确认的内容标记“实验开始前需核验”。

若仓库已有 Unit 3 的 `feature_list.json`、task boundary、sprint contract 和 trace，应以其唯一 active 或 ready-for-verification feature 为教材主线。若尚无 U3 产物，生成指南必须说明：课堂执行 U4 前，由教师或学生填入 U3 实际 `feature_id` 和边界；生成 Agent只能提供基于仓库的推荐候选，不得编造已完成的 U3 状态。

## 2. Unit 4 教学目标

Unit 4 要把“完成”从 Agent 的主观声明变成可执行、可复核、可交接的关闭协议。

学生比较同一个 Unit 3 feature 的两轮完成判断，再选择适合的完成系统：

1. baseline completion：沿用 U3 边界，但没有 completion gate、E2E、clean state 和 handoff；
2. strong completion：运行明确的门禁、最小 E2E、证据、清洁状态和交接；
3. 依据两轮证据决定哪些完成控制保留、放松、合并或移除。

评分不看测试和模板数量。强完成系统是认真构建的对照样本；最终设计要说明哪些检查补上真实证据，哪些增加运行、复核或维护成本，并保持必要的业务安全和完成证据。

## 3. Unit 3 继承规则

U4 必须接住 U3 的同一个功能，不重新选择需求。指南必须要求学生记录并沿用：

- `feature_id` 和 behavior；
- 当前 state 和 evidence；
- allowed/forbidden files；
- task boundary 或 scope contract；
- sprint contract；
- 原验证方式和 trace；
- 当前分支、提交、Git 状态或起始 diff。

如课堂不得不换功能，必须先记录原因，并保证 baseline 与 strong completion 仍使用同一个新功能和同一起始条件，不能通过换简单任务制造改善。

## 4. 写教材前的完成风险分析

生成 Agent 必须针对所选 feature 判断：

- 哪种静态或单元检查能发现最基础错误；
- 哪种运行时或集成检查能证明目标入口可用；
- 最小真实用户路径是什么；
- 应验证哪些业务结果、权限或数据不变量；
- 哪些“看似通过”证据不足，例如只有 import、HTTP 200、页面打开或 mock；
- 哪些数据库、迁移、删除、上传、邮件、外部服务或跨角色行为必须禁止；
- 如何验证范围外区域未被触碰；
- 哪些证据能被下一位 Agent 独立复放。

门禁负担要与 feature 风险匹配，不得把一个小功能扩成全系统测试项目。

## 5. `u4_student.md` 固定结构

必须生成：

1. `# <repo-name> Unit 4 学生指南`
2. `## 目标`
3. `## 1. 继承 Unit 3 的小功能`
4. `## 2. 基线完成运行`
5. `## 3. 构建强完成系统`
6. `## 4. 最小端到端验证`
7. `## 5. 清洁状态和交接`
8. `## 6. 交接演练和强完成运行`
9. `## 7. 对比报告与最终设计`
10. `## 8. 交付物`
11. `## 9. 反误区`

指南使用中文，命令和路径保留原文。每轮必须提供可直接复制的提示词、输入、输出路径、判断指标和禁止行为。

## 6. 对照条件

指南要求 baseline 与 strong completion 尽量保持：

- 同一 repo、feature id 和 behavior；
- 同一起始代码状态或可复核 diff；
- 同类 Agent/模型；
- 相近时间预算；
- 相同工具权限；
- 同一 U3 allowed/forbidden files。

任何差异都记录，并在最终报告中分析是否影响结论。

## 7. 基线完成运行

指南必须生成仓库特定 copy-paste prompt，基于：

```text
你正在接手 Unit 3 的 <feature_id>：<behavior>。代码已经存在或部分存在。请在不新增 completion gate、E2E 协议、clean-state 检查和 handoff 协议的前提下，判断它是否可以标记为 passing。

只沿用当前仓库已有的 feature_list、allowed/forbidden files 和 task boundary，不要重新选择或扩大功能。记录运行了哪些检查、为什么能或不能 passing、缺少什么证据、下一步安全行动是什么，并把完整过程保存为 measurement_logs/baseline_completion_run.md。
```

观察并记录：

- 是否只凭静态阅读、import、单元测试、mock 或 HTTP 200 passing；
- 是否执行 runtime/integration；
- 是否验证真实业务结果和不变量；
- 是否留下证据路径；
- 是否检查工作树状态；
- 下一位 Agent 是否能接手；
- 判断不能 passing 时，是否清楚指出缺口。

## 8. 诊断基线完成判断

要求学生从以下视角分析 baseline：

- 验证对象：Agent 要证明哪个具体行为；
- 验证深度：证据是否覆盖真实业务风险；
- E2E 价值与成本：最小真实路径会补上什么证据；
- 清洁状态信心：下一位 Agent 是否能独立判断状态和下一步。

强完成系统应针对这些缺口设计。学生要同时记录它新增的运行、维护和复核负担，最后解释哪些控制值得保留。不能把 baseline 拒绝 passing 自动当作高质量判断，还要看它是否识别了真正缺口。

## 9. 三层完成门禁

指南必须要求学生创建：

- `completion_gate.md`
- `completion_gate.json`
- `scripts/verify_<feature-id>.py`，或适合仓库平台的等价脚本
- `verification_logs/<feature-id>_gate_result.md`

### 9.1 `completion_gate.md` 最低字段

```md
# 完成门禁: <feature id> <title>

## 功能和 Unit 3 来源
- Behavior:
- State before gate:
- feature_list / boundary / sprint contract:
- Allowed files:
- Forbidden files:

## Layer 1: 静态 / 单元
- Command:
- Expected:
- Actual:
- Evidence:

## Layer 2: 运行时 / 集成
- Command:
- Expected:
- Actual:
- Evidence:

## Layer 3: E2E / 用户流程
- Command or procedure:
- Expected:
- Actual:
- Evidence:

## Completion rule
- 三层全部通过
- Unit 3 边界未违反
- feature evidence 已更新
- clean state 已确认
- handoff 已完成

## Failure rule
- 任一层失败不得 passing
- 记录失败原因和下一步安全行动
```

### 9.2 `completion_gate.json` 最低结构

```json
{
  "feature_id": "F01",
  "feature_title": "",
  "required_layers": [
    {"name": "static_unit", "command": "", "expected": "", "actual": "", "passed": false, "evidence_file": ""},
    {"name": "runtime_integration", "command": "", "expected": "", "actual": "", "passed": false, "evidence_file": ""},
    {"name": "e2e_user_flow", "command_or_procedure": "", "expected": "", "actual": "", "passed": false, "evidence_file": ""}
  ],
  "completion_rule": {
    "all_layers_must_pass": true,
    "feature_list_evidence_required": true,
    "handoff_report_required": true,
    "clean_state_required": true
  }
}
```

### 9.3 完成和失败规则

只有三层全部通过、feature evidence 更新、U3 边界未违反、clean state 通过且 handoff 完成，才允许 `passing`。

任一层失败时保持 `active`；只有存在真实外部阻塞并满足课程状态规则时才使用 `blocked`。必须写下一步安全行动，不能只写 `failed`。

## 10. 最小 E2E

指南必须为实际 feature 设计仓库特定、最小但真实的 E2E。可使用测试客户端、HTTP/API flow、浏览器步骤、CLI 或仓库已有工具，不强制引入大型框架。

要求学生生成 `verification_logs/<feature-id>_e2e_result.md`，包含：

```md
# 端到端验证: <feature id>

## Context
- User/role:
- Entry:
- Required data:

## Steps
1.
2.
3.

## Expected business result
-

## Actual result
-

## Invariants and boundaries checked
- 权限或可见性：
- 数据/状态不变量：
- 范围外区域未触碰：

## Evidence
- Command/output:
- Response/screenshot:
- State check:

## Result
passing / failing
```

E2E 不能只证明页面返回 200；必须证明目标用户看到或获得正确业务结果，并检查仓库特定不变量。

## 11. Agent 可读错误

所有失败信息必须使用：

```text
WHAT: 失败了什么
WHY: 为什么阻塞完成
FIX: 下一位 Agent 首先检查什么
BOUNDARY: 修复时不得触碰什么
```

## 12. 清洁状态

指南必须要求创建 `session_exit_checklist.md`，至少检查：

```md
# 会话退出检查清单

- [ ] 构建或启动路径仍可用
- [ ] 必需测试通过
- [ ] runtime/integration 已记录
- [ ] E2E 已记录
- [ ] feature_list 状态和 evidence 已更新
- [ ] Git diff 已保存或明确无源码改动
- [ ] 没有临时 debug 文件
- [ ] 没有注释掉的死代码
- [ ] 没有修改无关文件
- [ ] 当前状态明确
- [ ] 下一步安全任务明确
```

根据仓库需要加入 PROGRESS/DECISIONS、生成物、数据库或外部服务检查，但不要制造与 feature 无关的仪式。

## 13. 交接协议和报告

指南必须要求创建：

- `handoff_protocol.md`
- `handoff_report.md`
- `quality_status.md`

### 13.1 `handoff_protocol.md`

说明 passing 前必须运行 gate、E2E、更新 evidence、完成 clean state 和 handoff；任一失败不得 passing。

### 13.2 `handoff_report.md`

至少包含：

```md
# 交接报告

## Repository state
- Branch / commit:
- Git diff evidence:
- Feature id / state:
- Last verification:

## Verification summary
| Layer | Command/procedure | Result | Evidence |
|---|---|---|---|
| Static/unit | | | |
| Runtime/integration | | | |
| E2E | | | |
| Clean state | | | |

## Changed files and scope reason
## Passed items
## Failed or missing items
## Known risks
## Next safe task
## Do not touch
```

### 13.3 `quality_status.md`

列出 feature 状态以及 gate、gate result、E2E、clean state、handoff 和 handoff drill 的路径与缺口。

## 14. 下一位 Agent 交接演练

指南必须嵌入：

```text
你是一个全新的 Agent。请只根据当前仓库内容判断目标 Unit 4 feature 的状态，不依赖口头解释。

请回答并引用证据路径：
1. 当前 feature 是否完成？
2. 完成证据在哪里？
3. 仓库是否处于明确的清洁状态？
4. 下一步最安全的任务是什么？
5. 哪些区域禁止触碰？

无法判断时写 unknown，并说明缺少什么。
```

保存 `measurement_logs/next_agent_handoff_drill.md`，记录是否找到状态、证据、风险和下一步，以及所需口头补充次数。

## 15. 强完成运行

指南必须生成仓库特定 copy-paste prompt，要求 Agent：

- 读取 U3 feature 和边界；
- 实际运行三层 gate，而不是只阅读 gate；
- 执行最小 E2E；
- 更新 feature evidence；
- 完成 session exit checklist；
- 更新 handoff 和 quality status；
- 任一条件失败不得 passing；
- 保存 `measurement_logs/final_gated_completion_run.md`。

## 16. 对比报告与独立评估

执行 Agent 不得自评。教师提供 `eval.md` 时，独立评分 Agent 只能使用运行日志、gate/E2E/clean/handoff 证据和 measurement notes；不得访问仓库或补证据。没有 eval 时记录缺失。

指南必须提供 copy-paste prompt，生成 `unit4_comparison_report.md`，比较 baseline 与 strong completion：

| 指标 | Baseline | Strong completion | Evidence |
|---|---|---|---|
| 过早 passing | | | |
| 缺失证据项 | | | |
| Runtime/integration 已执行 | | | |
| E2E 已执行 | | | |
| Clean state 明确 | | | |
| 交接口头补充次数 | | | |
| 可独立判断 passing | | | |

报告要把收益、成本和适用条件连接到运行证据。明确 gate、E2E、handoff 和 clean state 的保留、放松、合并或移除决定，以及什么新证据会使学生修改该决定。最终方案可以更轻，但仍须证明必要业务结果和安全边界。

## 17. 最低交付物

- `measurement_logs/baseline_completion_run.md`
- `measurement_logs/final_gated_completion_run.md`
- `completion_gate.md` / `completion_gate.json`
- 验证脚本和 gate result
- E2E result
- `session_exit_checklist.md`
- `handoff_protocol.md`
- `handoff_report.md`
- `quality_status.md`
- `measurement_logs/next_agent_handoff_drill.md`
- `unit4_comparison_report.md`

## 18. 反误区

必须包含：

- 不重新选择 U3 feature；
- 不把 import、单元测试或 HTTP 200 当作完整完成证据；
- 不写了 gate 却不执行；
- 不把最小 E2E 扩成全系统测试；
- 不用 handoff 文档代替验证证据；
- 不在工作树状态不明时 passing；
- 不把 U3 回滚实验重新作为 U4 主任务；
- 不因模板齐全就认定有效。

再加入目标仓库特有的 2–4 条误区。

## 19. 生成后的自检

生成 Agent 必须确认：

- 文件存在且章节齐全；
- 明确继承 U3 feature；若实际 feature 未知，使用待填占位而不伪造；
- baseline 与强完成条件分离，最终设计有证据支持；
- 三层 gate、最小 E2E、业务不变量和禁止区域针对真实仓库；
- 包含每轮执行、交接演练、最终运行和对比的 copy-paste prompts；
- gate 负担与 feature 风险匹配；
- 没有生成 teacher guide、eval 或评分答案；
- 没有修改目标源码。

最终答复列出指南路径、继承或推荐的 feature、最小 E2E 摘要和待教师核验项。
