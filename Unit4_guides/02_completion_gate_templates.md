# Unit 4 完成门禁模板

本文件是共享模板。学生需要把模板改成自己项目和 功能的真实版本，不能直接空填交付。

## `completion_gate.md`

```md
# 完成门禁: <功能 ID> <功能标题>

## 1. 功能
- 功能 ID:
- 行为：
- Unit3 来源：feature_list / sprint_contract / scope_contract 路径：
- Unit3 allowed_files:
- Unit3 forbidden_files:
- 门禁前当前状态：
- 门禁后目标状态：

## 2. 必需证据

### 层级 1: 静态 / 单元检查
- 命令：
- 预期结果:
- 实际结果:
- 证据文件:

### 层级 2: 运行时 / 集成检查
- 命令：
- 预期结果:
- 实际结果:
- 证据文件:

### 层级 3: 端到端 / 用户流程检查
- 命令或手工流程：
- 预期结果:
- 实际结果:
- 证据文件:

## 3. 完成规则

只有满足以下条件，功能才能标记为 `passing`：

- 第 1 层通过
- 第 2 层通过
- 第 3 层通过
- 没有引入已知回归
- feature_list 证据字段已更新
- 已写交接报告
- 会话退出检查清单通过

## 4. 失败规则

如果任一必需层级失败：

- 不要把功能标记为 passing。
- 保持功能状态为 `active` 或 `blocked`。
- 记录失败原因。
- 记录下一步建议行动。

## 5. 设计取舍检查

- 这个门禁是否刚好证明当前功能，而不是覆盖整个系统？
- 是否存在只增加工作量、但不增加证明力的检查？
- 如果下一位 Agent 只读本门禁和证据日志，是否能判断 passing / blocked？
```

## `completion_gate.json`

```json
{
  "feature_id": "F01",
  "feature_title": "",
  "required_layers": [
    {
      "name": "static_unit",
      "command": "",
      "expected": "",
      "actual": "",
      "passed": false,
      "evidence_file": ""
    },
    {
      "name": "runtime_integration",
      "command": "",
      "expected": "",
      "actual": "",
      "passed": false,
      "evidence_file": ""
    },
    {
      "name": "e2e_user_flow",
      "command_or_procedure": "",
      "expected": "",
      "actual": "",
      "passed": false,
      "evidence_file": ""
    }
  ],
  "completion_rule": {
    "all_layers_must_pass": true,
    "feature_list_evidence_required": true,
    "handoff_report_required": true,
    "clean_state_required": true
  },
  "final_state_allowed": "passing"
}
```

## 验证日志

```md
# 验证日志: <功能 ID>

## 摘要
- 功能:
- 日期：
- Agent/会话：
- 总体结果:

## 层级 1: 静态 / 单元
- 命令：
- 输出摘要:
- 是否通过：
- 证据:

## 层级 2: 运行时 / 集成
- 命令：
- 输出摘要:
- 是否通过：
- 证据:

## 层级 3: 端到端 / 用户流程
- 流程:
- 输出摘要:
- 是否通过：
- 证据:

## 失败分析
- 失败内容：
- 重要原因：
- 建议修复：
- 边界：
```

## 端到端验证报告

```md
# 端到端验证报告: <功能 ID>

## 路径
- 仓库：
- 功能:
- 用户角色：
- 入口：
- 所需数据：

## 步骤
1.
2.
3.

## 预期业务结果
-

## 实际结果
-

## 已检查不变量
-

## 证据
- 命令输出：
- 截图或响应摘录：
- 数据/状态检查：

## 结果
通过 / 失败

## E2E 取舍
- 是否缺少真实用户路径：
- 是否覆盖过度：
- 下一轮保留 / 压缩 / 删除：
```

## Agent 可读错误消息格式

```text
ERROR: <简短失败名称>

WHAT:
<失败了什么？>

WHY:
<为什么这会阻塞完成？>

FIX:
<下一位 Agent 应先检查哪里？>

边界：
<修复时不得改动什么？>
```

## 最终门禁完成运行 日志

```md
# 最终门禁完成运行

## 输入
- 功能:
- 完成门禁:
- 端到端计划：
- 清洁状态检查清单:
- 交接协议:

## Agent 声明
-

## 门禁执行
| 层级 | 结果 | 证据 |
|---|---|---|
| 静态 / 单元 | | |
| 运行时 / 集成 | | |
| 端到端 / 用户流程 | | |

## 完成判定
- 功能是否可标记为 passing:
- 证据路径:
- 如果不能标记为 passing，当前状态：
- 下一步安全行动：
```

## `unit4_comparison_report.md`

```md
# Unit 4 对比报告

## 1. 对比的运行
- 仓库:
- 功能:
- Unit3 功能来源:
- 基线日志:
- 最终日志:

## 2. 对照条件

| 条件 | 基线 | 最终 | 是否一致？ | 说明 |
|---|---|---|---|---|
| feature_id / 行为 | | | | |
| 起始代码状态或 diff | | | | |
| Agent/模型 | | | | |
| 时间预算 | | | | |
| 工具权限 | | | | |
| allowed/forbidden files | | | | |

## 3. 指标对比
| 指标 | 基线 | 最终 | 是否改善？ | 证据 |
|---|---|---|---|---|
| 过早完成声明 | | | | |
| 缺失证据项 | | | | |
| 运行时/集成检查已执行 | | | | |
| 端到端已执行 | | | | |
| 清洁状态明确 | | | | |
| 交接所需口头补充次数 | | | | |
| 是否可独立判断为 passing | | | | |

## 4. Soft Completion vs Hard Gate

| 判断项 | Soft completion | Hard gated completion | Evidence |
|---|---|---|---|
| 是否提前 passing | | | |
| 是否漏掉 runtime/E2E | | | |
| 是否漏掉证据路径 | | | |
| 是否漏掉清洁状态 | | | |
| 是否漏掉交接要求 | | | |
| hard gate 是否发现 soft 漏项 | | | |
| hard gate 是否过重 | | | |

## 5. Tradeoff Reflection

- 完成门禁是否刚好够用，还是过轻 / 过重？
- E2E 是否最小但真实，还是缺失 / 过度？
- handoff 是否足够下一位 Agent 接手，还是太短 / 太长？
- clean state 检查是否提供真实状态证据，还是流于仪式？
- 哪些完成判断可以保留 soft checklist，哪些必须 hard gate 化？
- 下一轮会保留、压缩或删除什么？

## 6. 结论

在同一仓库、同一功能下，加入 完成门禁、端到端验证和交接协议 后，Agent 的过早完成声明从 X 次降到 Y 次；缺失证据项从 X 项降到 Y 项；新 Agent 接手所需口头补充从 X 条降到 Y 条；当前功能是否 passing 可以由验证日志独立判断。
```
