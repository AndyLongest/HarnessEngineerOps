# VulpesCRM Unit 2 学生指南

## 目标

本单元要把 VulpesCRM 改造成更容易交接给新 Agent 的仓库。你的成绩不看 Markdown 数量，而看冷启动前后是否更快、更准、更少猜：从“源码侦察”变成“Harness 路由 + 定向核验”。

VulpesCRM 的重点是 CRM 入口、注册登录、报价、公司联系人、SQLite 状态文件和删除路由风险。

## 0. 学生先熟悉仓库

你对这个仓库也还陌生。正式做冷启动前测之前，先建立基本方位感：看一遍目录、`README.md`、依赖文件、启动入口和主要源码文件，初步判断它是什么系统、如何启动、数据可能在哪里、哪些操作可能会写入状态。

接着请你自己尝试把仓库跑起来。优先按照仓库已有说明安装依赖、启动服务、打开首页或登录页；如果启动失败，就记录失败命令、报错信息和你认为缺失的说明。这个过程的目的不是立刻修项目，而是让你亲身体会：一个陌生开发者或新 Agent 接手时，会在哪些地方卡住。

这一轮熟悉只服务于你理解实验对象。除非启动项目本身必须产生本地运行状态，不要修改源码，不要主动删除、重置或迁移数据库，也不要把你的理解告诉执行冷启动的 Agent。前测时，执行 Agent 只能依赖仓库内容本身，这样测出来的 baseline 才真实。

## 1. 冷启动前测

先不要改仓库。把下面提示词交给一个全新的 Agent，不要补充口头背景。

```text
你是一个全新的 coding agent。你没有任何外部背景。
请只基于当前仓库内容完成冷启动重建任务。不要修改任何文件，除了按本提示词最后一行保存冷启动输出。

请回答：
1. 这是一个什么系统？
2. 技术栈是什么？
3. 如何安装依赖？
4. 如何启动项目？
5. 如何注册 / 登录？
6. 数据库或初始数据从哪里来？
7. 主要业务对象有哪些？
8. 如果要继续改造，下一步安全任务是什么？
9. 哪些文件或行为不能随便改？

回答末尾附上 Cold Start Trace：
- Start time / End time
- Files inspected
- Commands run
- Searches performed
- Uncertain points
- Assumptions made
- Evidence paths

请把完整回答保存为 measurement_logs/baseline_cold_start.md。
```

## 2. 记录指标

记录冷启动耗时、Q1-Q8 答对率、下一步安全任务是否准确、口头补充次数、文件读取数、工具调用次数、不确定表达数量，以及是否优先读取 Harness 入口文件。所有指标只和本仓库的后测比较。

## 3. 独立评分

前测和后测都不要让执行 Agent 自评。把教师提供的 `eval.md`、冷启动输出和你的测量记录交给另一个 Agent，由它只根据材料评分。请直接使用下面的 prompt：

```text
你是一个独立的 Harness 冷启动评估 Agent。
你没有参与这个仓库的改造，也不要使用外部背景知识。

我会给你三份材料：
1. eval.md：教师提供的标准答案、评分规则和指标抽取规则。
2. baseline_cold_start.md、detailed_doc_cold_start.md 或 final_cold_start.md：执行 Agent 的本轮冷启动输出。
3. measurement_notes：学生记录的本次测量信息，至少包括本轮是 baseline、detailed-doc 还是 final，以及口头补充次数；如果冷启动输出缺少 Start/End time，也在这里补充。

请只根据这些材料评分，不要访问仓库，不要替执行 Agent 补全答案。输出必须包含：
- Q1-Q8 每题得分：1 / 0.5 / 0，并说明依据
- 关键问题答对率：/8
- Q9 风险识别：是 / 部分 / 否
- 下一步安全任务是否准确：是 / 否
- 冷启动耗时
- 口头补充次数
- 文件读取数：unique files inspected
- Commands run 数量和列表
- Searches performed 数量和列表
- Tool calls 总量，如果能从 trace 推断
- 不确定表达数量
- 明确误判数量
- Assumptions made 数量或列表
- Evidence path quality：弱 / 中 / 强
- Harness-first 路由程度：低 / 中 / 高
- 主要扣分点
- 最需要补强的指导缺口

请把完整评分结果保存为：
- 如果输入是 baseline_cold_start.md：measurement_logs/baseline_eval.md
- 如果输入是 detailed_doc_cold_start.md：measurement_logs/detailed_doc_eval.md
- 如果输入是 final_cold_start.md：measurement_logs/final_eval.md
```

## 4. 详细文档系统实验

先不要直接追求“最终版本”。先把前测结果当成“文档不足时 Agent 会怎样”的证据。

然后创建一个认真、准确、但偏详细的文档系统。这个版本可以包含根入口、运行说明、项目地图、数据库状态、业务对象、风险、模块或流程文档；也可以使用嵌套 docs 目录，把 setup、architecture、workflow、module、risk 分开写。不要故意写错信息，也不要机械堆文件。每个重要事实都应该能回到源码证据。

用同一个冷启动提示词让全新的 Agent 复测详细版本，保存为：

```text
measurement_logs/detailed_doc_cold_start.md
measurement_logs/detailed_doc_eval.md
```

## 5. 特别注意

你现在不需要完全掌握 VulpesCRM 的每一行代码。Unit 2 的重点是找出“新 Agent 最容易迷路的地方”，再把这些信息写到它能稳定找到的位置。对这个仓库来说，最容易迷路的是：入口文件在哪里、CRM 的核心对象是什么、SQLite 状态文件是否能动、注册登录和删除路由有什么风险。

比较前测和详细版本时，重点看 Agent 能力变化：是否不再乱猜默认账号，是否更准确地定位 `database/crm.db`，是否理解报价/联系人主线，是否识别删除路由和数据库状态风险。也要看详细文档有没有引入新问题：重复说明、让源码证据变得更难找、或让 Agent 对未核验的 DB 状态过度自信。

## 6. 改进并最终复测

根据两次运行结果，保留真正改善 Agent 冷启动的文档，合并或删除没有带来能力改善的文档。不要因为某个文件在参考层级里出现就保留它，也不要因为“越短越好”就删掉有用的规则。

新开一个 Agent 会话，使用同一份冷启动提示词复测最终版本，只把保存路径改为：

```text
请把完整回答保存为 measurement_logs/final_cold_start.md。
```

复测时仍然不要口头解释仓库。

独立评分后保存：

```text
measurement_logs/final_eval.md
```

最终版本不是把详细版本简单缩短。逐项检查每个保留、合并或删除的文档：它修复了哪条 baseline 失误，是否在 detailed-doc 运行中改变了 Agent 行为，以及它带来的阅读、重复和维护成本。没有运行证据支持的复杂度，不应默认保留。

## 7. 对比与反思

生成 `measurement_logs/metrics_comparison.md`，比较 baseline、detailed-doc 和 final 三种状态。结论必须说明 final 是否更适合交接给新 Agent，以及为什么这个文档系统适合 VulpesCRM。

请直接使用下面的 prompt 生成最终对比报告：

```text
你是 Harness Unit2 的最终对比报告 Agent。

我会给你这些材料：
1. measurement_logs/baseline_eval.md：独立评分 Agent 对前测冷启动的评分。
2. measurement_logs/detailed_doc_eval.md：独立评分 Agent 对详细文档版本的评分。
3. measurement_logs/final_eval.md：独立评分 Agent 对最终版本的评分。
4. measurement_logs/baseline_cold_start.md、measurement_logs/detailed_doc_cold_start.md 和 measurement_logs/final_cold_start.md：三次冷启动原始输出。
5. measurement_notes：学生记录的补充指标，包括口头补充次数、缺失时间、异常情况。
6. 本次保留、合并、删除或改写的 Harness 文档清单，必要时包括关键片段。

请只根据这些材料生成 measurement_logs/metrics_comparison.md，不要替执行 Agent 补全答案，也不要把文档数量当成改造成绩。

报告必须包含：
- 一张 baseline vs detailed-doc vs final 指标表，至少比较：冷启动耗时、Q1-Q8 答对率、Q9 风险识别、下一步安全任务、口头补充次数、文件读取数、Commands run、Searches performed、Tool calls、不确定表达、明确误判、Evidence path quality、Harness-first 路由程度。
- 详细文档版本让 Agent 哪些能力改善；每条结论都要引用输出或评分证据。
- 详细文档版本引入了哪些新成本或维护风险。
- 最终版本保留、合并、删除了什么，以及原因。
- 对“final 是否更适合交接给新 Agent”的明确结论：是 / 部分是 / 否。
- 反思：这次实验改变了你对文档系统设计的什么判断？什么原则可以迁移到另一个仓库？

请把完整报告保存为 measurement_logs/metrics_comparison.md。
```

## 8. 交付物

- `measurement_logs/baseline_cold_start.md`
- `measurement_logs/baseline_eval.md`
- `measurement_logs/detailed_doc_cold_start.md`
- `measurement_logs/detailed_doc_eval.md`
- 最终保留的 Harness 文档系统
- `measurement_logs/final_cold_start.md`
- `measurement_logs/final_eval.md`
- `measurement_logs/metrics_comparison.md`

## 9. 反误区

不要把 Unit 2 理解成“写越多文档越好”。好的 Harness 是最小但完备：入口短、专题清楚、信息靠近代码、风险明确。不要为了后测好看给 Agent 口头补课；不要把一个超长 `AGENTS.md` 写成百科全书；不要在测量阶段改 `database/crm.db`；不要让 Agent 解释全源码。目标是让它先找到路，再定向核验。
