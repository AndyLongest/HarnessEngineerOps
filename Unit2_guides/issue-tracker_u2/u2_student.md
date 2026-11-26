# issue-tracker Unit 2 学生指南

## 目标

本单元要让新 Agent 更快理解 issue-tracker 的页面路由、登录会话、任务归属、共享权限和 API。成绩看冷启动前后指标改善，不看文档数量。

本流程仍然以“搭建最小可用 harness”为主。最后对比报告里会有一个简短的 Tradeoff Reflection，用来回看新增文档是否刚好够用，还是过长、过碎或太像源码复述；这不是新增大任务，只是复盘时做一次设计判断。同时标出哪些内容只是软约束或导航约束，哪些风险以后应该在 Unit3 变成硬约束。

## 0. 学生先熟悉仓库

你对这个仓库也还陌生。正式做冷启动前测之前，先建立基本方位感：看一遍目录、`README.md`、依赖文件、启动入口和主要源码文件，初步判断它是什么系统、如何启动、数据可能在哪里、哪些操作可能会写入状态。

接着请你自己尝试把仓库跑起来。优先按照仓库已有说明安装依赖、启动服务、打开首页或登录页；如果启动失败，就记录失败命令、报错信息和你认为缺失的说明。这个过程的目的不是立刻修项目，而是让你亲身体会：一个陌生开发者或新 Agent 接手时，会在哪些地方卡住。

这一轮熟悉只服务于你理解实验对象。除非启动项目本身必须产生本地运行状态，不要修改源码，不要主动删除、重置或迁移数据库，也不要把你的理解告诉执行冷启动的 Agent。前测时，执行 Agent 只能依赖仓库内容本身，这样测出来的 baseline 才真实。

## 1. 冷启动前测

改仓库之前，先把下面提示词交给一个全新的 Agent。

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

记录冷启动耗时、Q1-Q8 答对率、下一步安全任务、口头补充次数、文件读取数、工具调用次数、不确定表达数量和 Harness-first 路由。只比较 issue-tracker 的前测和后测。

## 3. 独立评分

把教师提供的 `eval.md`、冷启动输出和测量记录交给无关 Agent。评分 Agent 不能访问仓库，不能替执行 Agent 脑补答案。请直接使用下面的 prompt：

```text
你是一个独立的 Harness 冷启动评估 Agent。
你没有参与这个仓库的改造，也不要使用外部背景知识。

我会给你三份材料：
1. eval.md：教师提供的标准答案、评分规则和指标抽取规则。
2. baseline_cold_start.md 或 final_cold_start.md：执行 Agent 的冷启动输出。
3. measurement_notes：学生记录的本次测量信息，至少包括 baseline/final、口头补充次数；如果冷启动输出缺少 Start/End time，也在这里补充。

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
- 最需要补强的仓库工件

请把完整评分结果保存为：
- 如果输入是 baseline_cold_start.md：measurement_logs/baseline_eval.md
- 如果输入是 final_cold_start.md：measurement_logs/final_eval.md
```

## 4. 改造任务链

这一部分不是让你“补几篇 Markdown”凑数量，而是把仓库外、脑子里、口头解释里的关键信息放回项目中，让仓库本身成为 Agent 的事实来源。以后新的 Agent 接到开发任务时，可以先读这些入口和专题文档，快速知道项目怎么启动、业务对象是什么、哪些地方危险，再把上下文预算用在真正的功能开发上。

推荐做法是：`AGENTS.md` 只做短入口和路由，不写成百科全书；`RUNBOOK.md`、`PROJECT_MAP.md`、`DATA_MODEL.md` 等专题文档按需展开。这样既能降低冷启动发现成本，也能提高后续开发效率。

请仔细关注下表中的每一个文件，一个一个补齐。每补完一个文件，都要问自己三件事：它补上了哪个冷启动缺口？它让 Agent 少猜了什么？后测中应该从哪个回答或指标看出改善？如果答不上来，说明这个文件还只是空壳，需要继续改。

| 顺序 | 工件 | 要解决的问题 |
|---|---|---|
| 1 | `AGENTS.md` | 教材角色：仓库的“地图首页”。<br>解决缺口：不知道先读页面、数据库还是 API。<br>后续收益：不用一上来全文扫 `app.py`。 |
| 2 | `RUNBOOK.md` | 教材角色：开工说明书。<br>解决缺口：本地启动和 Docker 路径不清楚。<br>后续收益：不用反复试命令、猜端口和入口。 |
| 3 | `PROJECT_MAP.md` | 教材角色：目录导览。<br>解决缺口：页面、数据库、API、模板位置混在一起。<br>后续收益：降低翻源码找线索的成本。 |
| 4 | `DATA_MODEL.md` | 教材角色：权限关系地图。<br>解决缺口：不清楚谁能看谁的任务。<br>后续收益：避免混淆 owner 和 shared user。 |
| 5 | `API_MAP.md` | 教材角色：API 路线图。<br>解决缺口：不知道页面和 API 是否同一套权限规则。<br>后续收益：避免只改页面、不管 API 权限。 |
| 6 | `SMOKE_TEST.md` | 教材角色：最小安全验证。<br>解决缺口：不知道怎样证明项目能跑。<br>后续收益：不靠删除或重置数据库来验证。 |
| 7 | `KNOWN_RISKS.md` | 教材角色：危险路段提示牌。<br>解决缺口：不知道哪些操作不能随手做。<br>后续收益：避开数据库、删除、更新、取消共享风险。 |

## 5. 特别注意

你现在不需要完全掌握 issue-tracker 的每一行代码。Unit 2 的重点是找出“新 Agent 最容易迷路的地方”，再把这些信息写到它能稳定找到的位置。对这个仓库来说，最容易迷路的是：本地启动和 Docker 的关系、页面路由和 API 的关系、任务归属和共享权限、数据库状态文件是否能动。

写文档时要像画地图：先标主路，再标危险路段，不要把所有细节都塞进入口文件。能帮助 Agent 做决策的信息要写；只是复述源码、堆术语、写很长背景的内容不要写。

## 6. 最终复测

新开 Agent，用同一冷启动提示词复测，只把保存路径改成：

```text
请把完整回答保存为 measurement_logs/final_cold_start.md。
```

## 7. 对比报告

生成 `measurement_logs/metrics_comparison.md`，比较前后耗时、答对率、口头补充、文件读取、工具调用、不确定表达和 Harness-first 路由。结论要说明新 Agent 是否更容易接手。

请直接使用下面的 prompt 生成最终对比报告：

```text
你是 Harness Unit2 的最终对比报告 Agent。

我会给你这些材料：
1. measurement_logs/baseline_eval.md：独立评分 Agent 对前测冷启动的评分。
2. measurement_logs/final_eval.md：独立评分 Agent 对后测冷启动的评分。
3. measurement_logs/baseline_cold_start.md 和 measurement_logs/final_cold_start.md：前后两次冷启动原始输出。
4. measurement_notes：学生记录的补充指标，包括口头补充次数、缺失时间、异常情况。
5. 本次新增或改进的 Harness 工件清单，必要时包括关键片段。

请只根据这些材料生成 measurement_logs/metrics_comparison.md，不要替执行 Agent 补全答案，也不要把文档数量当成改造成绩。

报告必须包含：
- 一张 baseline vs final 指标表，至少比较：冷启动耗时、Q1-Q8 答对率、Q9 风险识别、下一步安全任务、口头补充次数、文件读取数、Commands run、Searches performed、Tool calls、不确定表达、明确误判、Evidence path quality、Harness-first 路由程度。
- 哪些 Harness 工件最可能带来了改善；每条结论都要引用前后输出或评分中的证据。
- 仍然没有改善或变差的指标，以及可能原因。
- 对“final 是否更适合交接给新 Agent”的明确结论：是 / 部分是 / 否。
- 下一轮最应该补强的 1-3 个仓库工件。
- Tradeoff Reflection：哪个 Harness 工件最明显提高了冷启动质量？有没有哪个工件过长、过碎或太像源码复述？哪些信息只是软约束或导航约束？哪些风险以后应变成 Unit3 硬约束？下一轮会保留、压缩或删除什么？

请把完整报告保存为 measurement_logs/metrics_comparison.md。
```

## 8. 交付物

- `measurement_logs/baseline_cold_start.md`
- `measurement_logs/baseline_eval.md`
- 新增或改进的 Harness 工件
- `measurement_logs/final_cold_start.md`
- `measurement_logs/final_eval.md`
- `measurement_logs/metrics_comparison.md`

## 9. 反误区

不要把 Unit 2 理解成“写越多文档越好”。好的 Harness 是最小但完备：入口短、专题清楚、信息靠近代码、风险明确。不要为了后测好看给 Agent 口头补课；不要把一个超长 `AGENTS.md` 写成百科全书；不要让执行 Agent 自评；不要删除任务或重建 `items.db`。目标是让它先找到路，再定向核验。
