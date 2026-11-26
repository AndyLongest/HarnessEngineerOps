<!-- Intent: Route instructors to the course materials and explain the revised teaching experiments. Updated: 2026-11-26. Upstream base: 2396734. Contribution sources: 6834912, 4c417d4, d4be79f, ed902d3. -->
# Harness Engineering course resources

本课程训练学生设计适合当前任务、风险和协作成本的 Harness。学生通过真实 Agent 运行比较不同设计，再用日志、diff、独立评估和反思解释哪些结构值得保留。

## 教学入口

| 单元 | 教材 | 实践入口 | 对照设计 |
|---|---|---|---|
| Unit 0 | [任务交代](Harness_Unit0_Tutorial.pdf) | 教材内练习 | 将模糊请求改成有对象、材料、限制和输出要求的任务 |
| Unit 1 | [失败诊断](Harness_Unit1_Tutorial.pdf) | 教材内练习 | 依据具体失败区分模型、上下文、执行环境和反馈问题 |
| Unit 2 | [项目可见与可接手](Harness_Unit2_Tutorial.pdf) | [总览](Unit2_guides/00_overview.md) · [生成协议](Unit2_guides/01_unit2_shared_protocol.md) | baseline → 详细文档 → 改进后复测 |
| Unit 3 | [范围与权限控制](Harness_Unit3_Tutorial.pdf) | [总览](Unit3_guides/00_overview.md) · [生成协议](Unit3_guides/01_unit3_shared_protocol.md) | baseline → 高控制 → 最终设计判断 |
| Unit 4 | [完成与交接](Harness_Unit4_Tutorial.pdf) | [总览](Unit4_guides/00_overview.md) · [生成协议](Unit4_guides/01_unit4_shared_protocol.md) | 轻验证 → 强完成系统 → 最终设计判断 |

Unit 2–4 各有五个项目包。每个 `<project>_uN/` 目录含 `uN_student.md`、`uN_teacher.md` 和 `uN_eval.md`，分别用于学生执行、教师观察和独立评估。生成协议可用于分析其他仓库并创建自包含的学生指南。

## 本次课程调整

Unit 2 增加准确但详细的文档对照版本。Unit 3 和 Unit 4 将单独的 soft 运行改为高结构对照与开放的最终取舍。学生需要解释行为改善、未解决问题、新增负担和适用边界；最终方案可以保留、放松、合并或删减控制。

各轮使用同一仓库和可比任务，记录模型、工具权限、预算、提示词、源码起点与人工补充的变化。Unit 4 沿用同一个 Unit 3 feature。将观察结果与效果归因分开报告。

## 文档维护

本次改变的是项目练习、教师/eval 指南、生成协议、对比模板和复杂度参考。新增参考说明不同设计强度的收益与成本。学生通过各项目指南取得完整执行步骤；教师应按角色分发资料。

原有 `completion_report.md` 记录早期教材生成状态。当前教学流程以本入口、共享协议和项目指南为准。

## 校验记录

2026-11-26 对本次 57 个 Markdown 文件完成相对链接和代码围栏检查；45 份项目指南覆盖三个单元、五个项目和 student/teacher/eval 三种角色。`git diff --cached --check` 通过。对照检查覆盖共享生成协议、项目指南、教师/eval 指南和比较模板的运行阶段及交付物。此记录是文档结构与内容对齐检查；课堂运行效果由实际实验记录报告。
