# Unit 2 新仓库学生教材生成协议

## 0. 用途

本文件是一份自包含的 Unit 2 教材生成协议。生成 Agent 只需要本文件、一个目标仓库和一句简单提示词，就应能够生成：

`Unit2_guides/<repo-name>_u2/u2_student.md`

不要假设 Agent 可以读取其他 overview、scope notes、模板、示例教材、teacher guide 或 eval。只生成学生指南，不生成评分答案，不修改目标项目源码。

推荐提示词：

```text
请严格按照《Unit 2 新仓库学生教材生成协议》，分析 <目标仓库路径>，生成该仓库的 u2_student.md。只生成学生指南，不修改项目源码；完成后执行协议中的自检。
```

## 1. 生成边界

先阅读目标仓库，再设计教材。不得只根据 README、仓库名或技术栈套用模板。

除目标 `u2_student.md` 外，不修改源码、配置、数据库、依赖、迁移、静态资源或现有 Harness 文件。优先静态核对安装、入口、数据和风险；不能安全确认的内容标记“实验开始前需核验”，不得猜测。

所有教材路径使用相对目标仓库根目录的真实路径。必须区分：

- 仓库事实：有源码、配置或文档证据；
- 教学设计：为 Unit 2 选择的实验步骤；
- 待核验项：静态阅读无法确定的运行事实。

## 2. 写教材前的仓库画像

生成 Agent 必须确认：

- 系统用途、主要用户和核心业务流；
- 安装、启动、测试和安全只读检查入口；
- 注册、登录、测试账号或初始化数据要求；
- 核心业务对象及关系；
- 页面、路由、API 或命令到真实文件的映射；
- 数据库、上传、缓存、生成物和状态文件位置；
- 初始化、迁移、删除、更新、重置和外部服务风险；
- static、vendor、generated、build、dist、media、migrations 等噪声目录；
- 已有文档、测试、脚本、CI 和 Harness 工件；
- 当前 Git 状态可能造成的实验干扰。

### 2.1 范围判断

- 小型仓库：入口少、业务流有限，可做全仓库 Unit 2。
- 中型仓库：围绕一条核心业务流建立 Harness，避免百科式文档。
- 大型或高噪声仓库：必须要求学生创建 `scope_contract.md`，写明模块、角色、页面/API、数据对象、启动/验证路径和排除区域。

不要只按文件数量判断规模。不要跨仓库比较耗时和文件读取数；只比较同一仓库 baseline 与 final。

## 3. Unit 2 教学目标

Unit 2 要让新 Agent 从“源码侦察”转为“Harness 路由 + 定向核验”。成绩不看 Markdown 数量，而看新 Agent 是否：

- 更快找到正确入口；
- 更准确理解业务和数据；
- 更少猜测和口头补充；
- 更早识别风险；
- 能提出安全的下一步任务。

实验比较 baseline、准确但详细的文档系统、根据证据改进后的 final 三种状态。详细版本是认真构建的对照样本；最终版本必须解释哪些指导改善了 Agent 行为，哪些只增加阅读、复核和维护成本。参考层级可帮助设计实验，但学生指南必须自行说明所需步骤。

Unit 2 可以说明软约束与硬约束的区别，但不进行正式控制实验。导航、提醒和风险说明通常是软约束；allowed/forbidden files、permission matrix、approval stop 和 sprint contract 留到 Unit 3。

## 4. `u2_student.md` 固定结构

必须生成以下章节：

1. `# <repo-name> Unit 2 学生指南`
2. `## 目标`
3. `## 0. 学生先熟悉仓库`
4. `## 1. 冷启动前测`
5. `## 2. 记录指标`
6. `## 3. 独立评分`
7. `## 4. 详细文档系统实验`
8. `## 5. 特别注意`
9. `## 6. 改进并最终复测`
10. `## 7. 对比与反思`
11. `## 8. 交付物`
12. `## 9. 反误区`

指南使用中文，命令和文件名保留原文。每一步说明目的、Agent 输入、输出路径、指标及禁止行为。

## 5. 学生先熟悉仓库

让学生查看目录、README、依赖、入口、核心源码和状态位置，并尝试安全启动或只读检查。此阶段不得修改源码、删除或重置数据，也不能把自己的理解告诉 baseline 执行 Agent，否则会污染前测。

大型仓库必须先区分业务代码与 static/vendor/generated/migrations 等噪声。

## 6. 冷启动前测

指南必须提供可直接复制的仓库特定提示词，基于下面模板改写：

```text
你是一个全新的 coding Agent，没有任何外部背景。请只根据当前仓库内容完成冷启动重建任务。除保存本次输出外，不要修改任何文件。

请回答：
1. 这是什么系统，主要用户和流程是什么？
2. 如何安装依赖？
3. 如何安全启动或运行最小只读检查？
4. 注册、登录、测试账号或初始化数据有什么要求？
5. 数据库、状态文件、上传或生成数据在哪里？
6. 核心业务对象和关系是什么？
7. <加入一个该仓库最关键的路由、权限或业务问题>
8. 下一步最安全的小任务是什么？
9. 哪些文件、数据或操作不能随便改？

回答末尾附上 Cold Start Trace：
- Start time / End time
- Files inspected
- Commands run
- Searches performed
- Uncertain points
- Assumptions made
- Evidence paths

把完整回答保存为 measurement_logs/baseline_cold_start.md。
```

问题必须能从仓库证据判断，且三轮完全相同。详细文档复测只把输出改为 `measurement_logs/detailed_doc_cold_start.md`；最终复测改为 `measurement_logs/final_cold_start.md`。每轮使用全新会话，保留模型、权限、预算和口头补充记录。

## 7. 指标与记录

要求学生记录：

- 冷启动耗时；
- Q1–Q8 关键问题准确度；
- Q9 风险识别；
- 安全下一步是否准确；
- 口头补充次数；
- unique files inspected；
- 工具调用数；
- 不确定表达数；
- 是否先读 Harness，再定向核验源码。

缺少记录时写 `未记录 / 不可判定`，不得写成 0。

## 8. 独立评分

执行 Agent 不得自评。指南必须提供 copy-paste prompt，要求无关评分 Agent 只使用：

1. 教师提供的 `eval.md`；
2. baseline、detailed-doc 或 final 本轮的 cold-start 输出；
3. `measurement_notes`。

评分 Agent 不得访问仓库、使用外部知识或替执行 Agent 补证据。教师没有提供 `eval.md` 时应暂停评分并记录缺失，不得自创标准答案。

保存：

- `measurement_logs/baseline_eval.md`
- `measurement_logs/detailed_doc_eval.md`
- `measurement_logs/final_eval.md`

评分输出至少包含 Q1–Q8 得分、Q9 风险识别、安全下一步、耗时、口头补充、文件读取、工具调用、不确定表达和主要缺口。

## 9. 详细文档系统实验

先根据 baseline 缺口构建准确、可追溯但较详细的指导系统。从下列工件选择有实际内容的集合，允许较细的专题或流程层级，以观察详细指导的收益和成本：

- `AGENTS.md`：最短入口、阅读顺序和安全边界；
- `RUNBOOK.md`：安装、启动、停止、测试和常见失败；
- `PROJECT_MAP.md`：业务流到真实文件路径的映射；
- `ARCHITECTURE.md`：仅在架构确实复杂时创建；
- `DATA_MODEL.md`：对象、关系、写入和不变量；
- `TASKS.md`：安全候选任务与非目标；
- `SMOKE_TEST.md`：最小、只读或可回滚的检查；
- `KNOWN_RISKS.md`：仓库特定危险状态和操作；
- `scope_contract.md`：中大型或高噪声仓库的明确范围。

不得用错误事实或空文件制造反面样本。每个事实必须能核验到源码。用同一冷启动提示词复测，保存 `measurement_logs/detailed_doc_cold_start.md`，独立评分保存 `measurement_logs/detailed_doc_eval.md`。

指南必须要求学生先比较 baseline 与详细版本：哪些误判消失、哪些仍存在、哪些指导改变了读取路径，以及是否增加重复、噪音、过时风险和人工复核成本。再决定最终保留、合并、删减或改写哪些指导。更短或更长都需要证据支持。

Harness 设计需要讨论两组取舍：

- 一个巨型入口文件 vs 太多碎片文件；
- 信息太少导致猜测 vs 信息过多变成源码复述。

## 10. 最终复测与对比

根据两轮结果改进 Harness 后，用同一问题、相近 Agent/模型、时间预算和权限进行 final cold start，并独立评分。记录环境差异，不把模型或人工帮助变化直接归因于文档设计。

指南必须提供 copy-paste prompt，生成 `measurement_logs/metrics_comparison.md`。报告比较同一仓库 baseline、detailed-doc 与 final，并引用三轮 cold-start 输出、eval、measurement notes 和 Harness 变更。

至少回答：

- 哪些答案、风险识别和安全下一步改善；
- 是否减少无关探索，或让首批读取路径更合理；
- 口头补充是否减少；
- 哪个工件最有效；
- 是否有工件过长、过碎或接近源码复述；
- 哪些内容可以保持软约束，哪些风险应在 Unit 3 硬化。
- 最终保留、合并或移除了什么，以及运行证据支持的理由；
- 可以迁移到另一个任务的设计原则及其适用条件。

## 11. 最低交付物

- `measurement_logs/baseline_cold_start.md`
- `measurement_logs/detailed_doc_cold_start.md`
- `measurement_logs/final_cold_start.md`
- `measurement_logs/baseline_eval.md`
- `measurement_logs/detailed_doc_eval.md`
- `measurement_logs/final_eval.md`
- `measurement_logs/measurement_notes.md` 或等价记录
- 实际选择的最小 Harness 工件
- `measurement_logs/metrics_comparison.md`
- 大型仓库需要的 `scope_contract.md`

## 12. 反误区必须仓库特定化

至少提醒：

- 不要在 baseline 前创建最终 Harness；
- 不要把 README 重写当作 Harness 改善；
- 不要复制源码制造长文档；
- 不要用删除、重置、迁移或真实数据写入做 smoke test；
- 不要跨仓库比较原始指标；
- 不要编造启动命令、账号、数据位置或安全性结论。

再加入 2–4 条目标仓库特有误区。

## 13. 生成后的自检

生成 Agent 必须检查：

- 目标文件存在且章节齐全；
- 冷启动问题、路径、业务对象和风险来自真实仓库；
- 包含 baseline、detailed-doc、final、独立评分和对比的 copy-paste prompts；
- 详细版本事实准确，最终取舍同时讨论行为改善和新增负担；
- 范围策略与仓库规模匹配；
- 没有要求不必要的 Harness 文件；
- 没有生成 teacher guide、eval 或实验答案；
- 没有修改目标项目源码；
- 未确认事实已标记待核验。

最终答复列出学生指南路径、范围判断和待教师核验项。
