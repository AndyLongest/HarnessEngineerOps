<!-- Intent: Route assessors through the general design and evidence principles. Updated: 2026-11-26. Upstream base: 2396734. Contribution sources: d4be79f, 8a2038d, and the subsequent working-tree assessment reorganization. -->
# General assessment principles

本目录说明如何评价 Harness 设计取舍，以及如何从人类与 AI 的协作记录判断学习者实际展示了什么。设计有效性和个人能力证据分别报告，再通过可追溯证据说明它们的联系。

## 阅读顺序

| 材料 | 用途 |
|---|---|
| [Tradeoff design](tradeoff_design.md) | 设计可比较的任务，观察收益、成本和适用边界 |
| [Reflection-Eliciting Tasks workflow](reflection_eliciting_tasks_workflow.md) | 从不足、高结构对照和最终改进中引出有证据的设计判断 |
| [Harness Engineering K/M/R/I profile](profiles/harness_engineering/PROFILE.md) | 定义构念、知识范围、证据门槛与报告边界 |
| [Construct rules](profiles/harness_engineering/construct_rules.md) | 识别知识应用、调节过程、条件化判断和前瞻迁移 |
| [Human–AI session evidence assessment skill](session_evidence/SKILL.md) | 分析原始交互，再对产出与反思进行定性分析和逐项三角互证 |

## 使用方式

1. 给出具体任务说明、教授的知识点、初始条件和实际提供给学习者的模板或提示词。
2. 选择本目录的 K/M/R/I profile，并将任务知识和要求绑定到真实教学材料。需要数字评分时，另附该任务明确的量规条目和锚点。
3. 收集原始交互、工具结果、工件/diff、运行证据、反思以及来源关系，记录缺失或局部覆盖。
4. 按 skill 分析会话中的学习者决策，分别检查产出和反思，再逐条记录互证、补充、矛盾或同源重复。
5. 分别报告 K、M1–M4、R、I 的证据强度、置信度、依据和局限，同时独立报告任务结果与设计成本。

## 来源与版本

设计取舍方法来自 linmou 的课程设计贡献，原始提交包括 `6834912`、`4c417d4`、`d4be79f` 和 `ed902d3`。K/M/R/I 构念与归因规则来自同一课程工作区后续的评估整理；本目录将它们组织为通用原则和任务驱动的 profile。

`session_evidence/` 是 [linmou/ai-augmented-expertise-assessment](https://github.com/linmou/ai-augmented-expertise-assessment) 在 `00e3b29ab329855705d9f044f16a246418c767b8` 的原样快照，skill 名称为 `agent-evidence-assessment`。更新时记录上游版本并核对 profile contract。各文档的源文件和校验结果见 [贡献记录](contribution_record.md)。
