# Unit 2 Guide Completion Report

Status: revised to one student guide, one teacher guide, and one independent eval file per repository.

## Reference Structure Used

The student guides now follow the structure of `Harness_Unit2_Task_Design - forstudent.docx`:

1. Baseline cold start before any edits
2. Metrics table
3. Independent scoring
4. Unit 2 task chain
5. Repository-specific focus
6. Final retest with the same prompt
7. Final comparison report prompt
8. Deliverables
9. Anti-misconceptions

## Generated Global Files

- `00_overview.md`
- `01_unit2_shared_protocol.md`
- `02_cross_repo_scope_notes.md`
- `completion_report.md`

## Repository Packages

| Repo | Student file | Teacher file | Eval file | Scope decision | Group recommendation |
|---|---|---|---|---|---|
| VulpesCRM | `student_guide.md` | `teacher_guide.md` | `eval.md` | Full-repo Unit 2 | Medium |
| issue-tracker | `student_guide.md` | `teacher_guide.md` | `eval.md` | Full-repo Unit 2 | Weak/medium |
| Inventory-Manager | `student_guide.md` | `teacher_guide.md` | `eval.md` | Full-repo Unit 2 | Weak |
| Python-Flask-Sqlite-RestApi-WebApp | `student_guide.md` | `teacher_guide.md` | `eval.md` | Scoped Unit 2 | Medium/strong |
| student-management-using-django | `student_guide.md` | `teacher_guide.md` | `eval.md` | Scoped Unit 2 | Strong |

## Distribution Rule

Each student should receive only the relevant `student_guide.md`. That file contains the full task flow they need.

Each teacher should use the relevant `teacher_guide.md`. The independent scoring Agent should receive `eval.md`, the cold-start output, and `measurement_notes` after baseline/final output exists. Do not give `eval.md` to the cold-start execution Agent.

## Files Needing Teacher Review

- Each `teacher_guide.md`, especially the eval answer table.
- Scoped guidance for `Python-Flask-Sqlite-RestApi-WebApp` and `student-management-using-django`.
- Any statement about default credentials or preloaded DB content before classroom use.

## Next Actions

1. Give each student group only its repo-specific `student_guide.md`.
2. Run baseline cold start and save `measurement_logs/baseline_cold_start.md`.
3. Use `eval.md` with an unrelated Agent to produce `baseline_eval.md`. Provide three inputs: `eval.md`, `baseline_cold_start.md`, and `measurement_notes` containing baseline/final label, oral supplement count, and missing Start/End time if needed.
4. Students add the recommended Harness artifacts inside their assigned repo.
5. Run final cold start with the same prompt and save `final_cold_start.md`.
6. Use the same eval rules plus final `measurement_notes` to produce `final_eval.md`.
7. Use the final comparison report prompt in the student guide to produce `metrics_comparison.md`. Compare baseline vs final metrics inside the same repo only.

Unit 2 grading should remain about cold-start improvement, not Markdown quantity.

`baseline_eval.md` and `final_eval.md` must include both Q1-Q8 scoring and all Unit 2 training metrics: cold-start time, safe next task accuracy, oral supplement count, files inspected, commands, searches, tool calls, uncertainty phrases, wrong claims, assumptions, evidence quality, and Harness-first routing.
