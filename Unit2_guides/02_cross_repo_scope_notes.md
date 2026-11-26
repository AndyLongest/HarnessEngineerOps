# Cross-Repo Scope Notes

Scoring reminder: Unit 2 is graded by cold-start improvement, not Markdown quantity.

## Small Repo Strategy

Small repos can usually be full-repo Unit 2 tasks. Students should map the whole app at a practical level: entry point, routes, data model, install/start steps, login or seed data, smoke path, and risky files/actions.

## Medium Repo Strategy

Medium repos should still avoid exhaustive explanation. Students should identify the most important business flow and give Harness routing that points to the exact files an Agent should verify.

## Large Repo Strategy

Large repos need an explicit `scope_contract.md`. The scope must say which module, flow, pages/APIs, tables, startup path, and verification path are in scope. It must also name what is out of scope.

## When To Use `scope_contract.md`

Use a real scope contract when the repository has many modules, many generated/static files, or multiple user roles/business flows. A small repo can simply state that full-repo Unit 2 is suitable.

## Why Large Repos Are Not Full-Repo Tasks

Unit 2 trains handoff quality, not encyclopedic documentation. Asking students to explain a large repository end to end pushes them toward shallow summaries and hides whether the Agent can actually route to the right files.

## Why File Count Cannot Be Compared Across Repos

File counts depend on framework, bundled static assets, screenshots, migrations, and templates. Compare only baseline vs final inside the same repo, and prefer “better first files inspected” over “fewer total files inspected” for large repos.
