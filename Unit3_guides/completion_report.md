# Unit 3 Guide Generation Completion Report

## Source Read

Read the real local `UNIT2_GUIDES` directory and used its project child directories as the source of truth:

- `Inventory-Manager`
- `issue-tracker`
- `Python-Flask-Sqlite-RestApi-WebApp`
- `student-management-using-django`
- `VulpesCRM`

For each project, the Unit 2 `student_guide.md`, `teacher_guide.md`, and `eval.md` were reviewed to extract scope decisions, repo risks, and student intensity.

## Created

Root files:

- `UNIT3_GUIDES/00_overview.md`
- `UNIT3_GUIDES/01_unit3_shared_protocol.md`
- `UNIT3_GUIDES/02_unit3_artifact_templates.md`
- `UNIT3_GUIDES/completion_report.md`

Project files:

- `UNIT3_GUIDES/<project>/student_guide.md`
- `UNIT3_GUIDES/<project>/teacher_guide.md`
- `UNIT3_GUIDES/<project>/eval.md`

## Student Guide Structure

The student guides now mirror the Unit 2 organization while preserving Unit 3's controllability focus:

1. Students familiarize themselves with the repository without priming the execution Agent.
2. Run an unconstrained baseline task.
3. Record controllability metrics.
4. Use an independent scoring Agent with `eval.md`.
5. Build the Unit 3 control artifact chain.
6. Note repo-specific risks.
7. Run the constrained final task.
8. Generate the final comparison report with the included prompt.
9. Deliver all run logs, evals, control artifacts, and comparison evidence.
10. Review anti-misconceptions.

The baseline task section now includes teaching rationale, not only an execution prompt. Each guide explains why the task was selected, how it can be split into candidate features, and which single feature should be used to demonstrate WIP=1 in the final run.

The guides also require a rollback harness before real Agent execution: create `scripts/unit3_git_safety.ps1`, run `bootstrap` once, and verify that a student can ask the Agent UI to rollback. The Agent should preserve `git diff`, restore the baseline changes, and report current status without the student manually typing the Git sequence.

The rollback harness is documented as an experiment safety tool only. It is not counted as a core Unit 3 control artifact for quality scoring.

This revision also tightens the evaluation model:

- Baseline prompts are natural product requests, without high-risk hints, allowed files, forbidden files, or Unit 3 trace templates.
- `forbidden violation` and `scope drift` are scored separately.
- Baseline scoring focuses on scope drift; final scoring focuses on boundary adherence.
- `measurement_notes` are required, and missing oral supplementation counts must be written as `未记录 / 不可判定`, not 0.
- Comparison reports must include scope drift analysis and cite evidence rather than scoring Markdown quantity.

## Guardrails Followed

- Did not modify `UNIT2_GUIDES`.
- Did not modify project source code.
- Created only `UNIT3_GUIDES` Markdown materials.
- Kept Unit 3 focused on controllability: WIP=1, `feature_list.json`, permission matrix, sprint contract, task trace, and baseline-vs-final evidence.

## Teaching Check

The guides are intentionally not Unit 2 repeats. They do not ask students to write more repo explanation docs. They ask students to prove that an Agent's behavior is more bounded and reviewable after adding control artifacts.
