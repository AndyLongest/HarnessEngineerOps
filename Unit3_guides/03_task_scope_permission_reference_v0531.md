# Task, Scope, And Permission Control Reference v0531

Intent: This file gives learners examples of Unit 3 execution-control complexity. These levels are reference points only, not standard answers and not required final designs. Every level contains the same four ideas: task decomposition, finish definition, complexity control, and safety-efficiency tradeoff. The difference is how explicit, fine-grained, and strict those ideas become.

## How To Read The Levels

Use these levels to compare Agent behavior under different control systems.

Do not choose the most detailed level by default. The sophisticated level is a serious high-control experiment. It can be necessary for complex or risky repos, but it can also slow execution, create paperwork, and make human review harder.

For each level, ask:

- Did the Agent understand the work unit?
- Did the Agent know what "finished" meant?
- Did the Agent avoid doing too many things at once?
- Did the safety rules reduce risk without blocking useful progress?

## Natural Request Only

The Agent receives a realistic product request and uses the repository as it is.

Example:

- "Make it easier for users to find the records they care about."
- "Improve the dashboard experience."
- "Make the list page more useful."

Task decomposition: The request is not decomposed. The Agent decides for itself whether the work is one feature, several features, a refactor, or a bug fix.

Finish definition: Finish is mostly implicit. The Agent may rely on "code changed," "tests ran," or a plausible explanation instead of evidence for one defined behavior.

Complexity control: There is no explicit limit on simultaneous work. The Agent may change UI, API, data shape, auth, config, and cleanup in one run.

Safety-efficiency tradeoff: This is fast to start and useful as a baseline, but it gives the Agent too much freedom. Human review often depends on reading the whole diff and guessing intent.

Typical signals:

- more than one feature starts
- nearby risky files are edited
- completion is claimed without enough evidence
- the run is hard to replay

## Single Coarse Feature

The broad request is rewritten into one feature statement, but finish, scope, permission, and trace remain light.

Example:

- "Add status filtering to the issue list."
- "Add a readonly search parameter to one existing API endpoint."
- "Improve the display of one student result page."

Task decomposition: The learner reduces the broad request to one named feature. Related possible features are still informal.

Finish definition: Finish is described in ordinary language, such as "users can filter by status," but evidence and stop conditions may remain vague.

Complexity control: The run is less broad than the natural request, but the Agent may still choose several implementation surfaces or variants inside the feature.

Safety-efficiency tradeoff: This is efficient for simple repos. It becomes risky when the named feature sits near auth, permissions, database files, migrations, generated files, or deployment config.

Typical signals:

- the Agent stays closer to one feature
- the Agent may still expand into nearby roles, routes, fields, or cleanup
- review is easier than baseline but still depends on interpretation

## Feature With Lightweight Finish And Boundary

The feature statement includes a simple finish definition and a rough boundary.

Possible shape:

- selected feature
- expected user-visible behavior
- one or two evidence requirements
- explicit non-goals
- rough allowed area
- rough forbidden area

Task decomposition: The learner keeps one feature and names nearby work that is not part of this run.

Finish definition: The Agent is told what observable behavior or verification evidence is enough to stop.

Complexity control: The boundary discourages obvious drift, but it may still be too broad for risky repos.

Safety-efficiency tradeoff: This keeps setup light while giving the Agent a clearer target. It may fail when the Agent encounters a tempting risky edit that was not explicitly classified.

Typical signals:

- the Agent can say what it will not do
- the diff mostly belongs to one behavior
- discovered related issues are more likely to be recorded instead of fixed

## Feature List With One Active Feature

The broad request is decomposed into a small set of candidate features, and exactly one may be active.

Possible shape:

- `feature_list.json`
- feature id
- feature state
- behavior
- finish evidence
- non-goals
- one-active-feature rule

Task decomposition: The learner separates the broad request into executable feature candidates. The final run chooses one.

Finish definition: Each candidate feature has its own finish evidence, so "done" is tied to the chosen feature rather than the whole broad request.

Complexity control: Work-in-progress is controlled. The Agent must leave other candidate features alone, even if they are reasonable future work.

Safety-efficiency tradeoff: This is stronger against parallel partial work. It costs more setup and can become artificial if a natural feature is split into fragments that cannot be tested meaningfully.

Typical signals:

- the Agent selects one feature instead of doing several
- related features are recorded but not started
- final output explains why the other features were left alone

## Contract-Controlled Feature Run

The selected feature has a scope contract, sprint contract, basic permission rules, and short trace.

Possible shape:

- one active feature
- `task_boundary.md`
- `sprint_contract.md`
- allowed edit areas
- forbidden areas
- actions that require approval
- short trace notes

Task decomposition: The chosen feature is translated into a concrete execution contract before editing starts.

Finish definition: Finish evidence is written into the contract, often with a stop state such as `ready_for_verification`.

Complexity control: The contract limits edit surface and records out-of-scope discoveries instead of letting the Agent absorb them.

Safety-efficiency tradeoff: This level is often a practical final system. It allows real implementation while blocking common overreach. It can become inefficient if the allowed area is too narrow or if too many routine actions require approval.

Typical signals:

- the Agent checks scope before editing
- approval-required actions stop before execution
- forbidden work is recorded as out of scope
- final output separates implemented work from blocked or deferred work

## Sophisticated Fine-Grained Control System

The learner builds a serious high-structure Unit 3 control system. This version should be accurate and plausible, not intentionally bad.

Possible shape:

- `feature_list.json` with several fine-grained candidate features
- exactly one active feature
- clear feature states such as `not_started`, `active`, `ready_for_verification`, and `blocked`
- each feature has behavior, finish evidence, non-goals, allowed area, risky neighbors, and stop condition
- `task_boundary.md` separates in-scope, out-of-scope, forbidden, and discovered-but-unfixed work
- `docs/policies/permission-matrix.md` separates `allowed`, `requires_human_approval`, and `forbidden` actions
- `docs/policies/human-approval-flow.md` tells the Agent when to stop and what evidence to provide
- `sprint_contract.md` must be filled before editing
- `logs/agent-runs/<feature-id>.md` records reads, edits, commands, permission checks, scope decisions, errors, verification attempts, and final state recommendation
- `measurement_logs/final_constrained_run.md` preserves the run summary for comparison

Task decomposition: The broad requirement is split into fine-grained features. The Agent must pick one and justify why the others are not started.

Finish definition: Each feature has explicit evidence, non-goals, and stop state. The Agent cannot treat partial implementation as completion.

Complexity control: Work-in-progress, edit surface, risky neighbors, and trace expectations are all controlled. Related problems are captured as out-of-scope notes, not pulled into the run.

Safety-efficiency tradeoff: This can match sophisticated test cases where a broad request can easily cross feature, role, API, database, permission, dependency, or deployment boundaries. It is safer and more reviewable, but it costs attention and maintenance.

Possible new problems:

- a natural feature is split so finely that implementation becomes artificial
- the Agent spends more attention satisfying forms than understanding the code
- the permission matrix blocks safe routine work
- the trace becomes long but not more useful
- the finish definition becomes a checklist that ignores real user behavior
- duplicated rules become hard for humans to review
- students mistake artifact quantity for control quality

Use this level as the serious "too much structure" experiment. If it improves safety and reviewability, keep the parts that caused the improvement. If it creates noise, delay, or brittle rules, merge, relax, or remove the parts that did not change Agent behavior.

## Choosing A Suitable Final System

The final Unit 3 system may be simpler than the sophisticated version.

A suitable design should answer:

- How is the broad request decomposed?
- What is the one executable feature for this run?
- What counts as finished?
- What nearby work is intentionally not part of the run?
- Where may the Agent read and edit?
- Which actions are allowed, approval-required, or forbidden?
- What evidence lets a human replay the run?

Do not score by artifact quantity.

Score whether the final Agent run is more bounded, more permission-aware, and easier to review than the under-controlled run, without keeping unnecessary burden from the sophisticated version.
