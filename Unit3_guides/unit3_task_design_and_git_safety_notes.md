# Unit3 任务设计与可撤销 harness 记录

本记录沉淀本轮对 Unit3 guide 的设计修正，供后续修改 Unit3 材料时参考。

## 1. Unit3 任务不能只是 prompt

无约束基线运行的 prompt 不是给学员机械复制的答案，而是一个教学刺激。Guide 必须让学员先理解：

- 这个任务来自仓库哪个真实工作流；
- 为什么它会诱发 Agent overreach；
- 它附近有哪些高风险文件、状态或业务边界；
- 它可以拆成哪 2-3 个 atomic feature；
- 最终 constrained run 为什么只能选择其中一个 active feature；
- 什么证据能说明这个 feature 到达 `ready_for_verification` 或 `passing`。

## 2. Unit3 的关键设计启发

Unit3 应聚焦这些 Harness 概念：

- WIP=1：任何时候只允许一个 feature active。
- 任务原子化：宽泛需求必须拆成单一行为。
- 功能清单三元组：每个 feature 至少包含行为描述、验证方式、当前状态。
- 范围外部化：边界不能只在对话里说，必须写入仓库工件。
- 完成证据：不能用“代码看起来完成”代替可复核验证。
- 过程可观测：读了什么、改了什么、为什么没做其他候选 feature，都要留下 trace。

## 3. 可撤销 harness 是 Unit3 开工前提

Unit3 的无约束基线运行会真实修改项目文件，而且它的目的之一就是观察 Agent 会不会越界。项目被改乱不是意外，而是实验可能发生的正常结果。

真实事故案例：学员让 Agent 做无约束基线任务，Agent 同时改了路由、模板和数据库初始化逻辑。改到一半 token 用完，会话停止，项目留下半截改动：页面打不开，数据库状态不确定，Agent 也没有完整说明自己为什么改这些文件。如果开工前没有可撤销 harness，后面只能手工猜哪些改动该删，整个项目基本废掉；如果有 harness，学生可以在聊天界面要求“回滚”，Agent 先保存 diff 作为实验材料，再撤回坏代码，课程可以继续。

因此：没有可撤销 harness，不要开始 Unit3 的真实 Agent 运行。这里的目标不是让学员背 Git 命令，而是让 Agent 能在聊天界面收到“回滚”请求后，自己保存 diff、撤销改动并报告状态。

## 4. 学员最低 harness 标准

在对应项目目录创建 `scripts/unit3_git_safety.ps1`。它至少要支持：

- `bootstrap`：建立 checkpoint 和实验分支；
- `rollback`：保存 diff、撤销改动、输出 `git status`；
- `status`：汇报当前工作树是否干净；
- `capture` / `restore`：作为底层动作供 Agent 拆开调用。

验收方式是在 Agent UI 里输入：

```text
请使用 rollback harness 回滚到基线运行前状态，并保留本轮 diff 证据。
```

Agent 应该自己调用 harness，生成 `measurement_logs/unit3_run_diff.patch`，恢复工作树，并说明当前状态。Unit4 不再重复讲可撤销主题；Unit4 专注完成门禁、E2E 证据、清洁状态和交接协议。
