# Verification And Completion Complexity Reference v0531

Intent: This file gives learners examples of verification and completion-system complexity. These are reference points only, not standard answers and not required final designs. Every level contains the same four ideas: verification target, verification depth, E2E value/cost, and clean-state confidence. The difference is how explicit, fine-grained, and strict those ideas become.

## How To Read These Examples

Use these examples to compare Agent behavior under different completion systems.

Do not choose the most detailed version by default. A strict completion system can be necessary for risky features, but it can also slow work, create noisy evidence, and make human review harder.

For each version, ask:

- Did the Agent know which behavior it had to prove?
- Did the evidence cover the real risk of this feature?
- Did E2E add useful proof, or only add ceremony?
- Could a next Agent judge the state without oral explanation?

## Code Looks Finished

The Agent reads the code or existing diff and decides whether the feature is complete.

Verification target: The target behavior is mostly implicit. The Agent may infer completion from changed files, plausible implementation, or its own summary.

Verification depth: Very light. It may inspect code, run no command, or run one shallow command.

E2E value/cost: No E2E. This is fast, but it does not prove the feature works in the real system.

Clean-state confidence: Weak. A next Agent often needs oral explanation to know what was tested, what failed, and whether the feature can be closed.

Typical signals:

- early `passing` recommendation
- evidence is mostly narrative
- no clear runtime or user-flow proof
- next Agent cannot find enough state from the repo alone

## Shallow Command Evidence

The Agent runs one or two familiar checks, such as import, lint, unit test, or a route/page smoke check.

Verification target: The feature is named, but the exact behavior may still be vague.

Verification depth: Better than reading only, but often still checks the environment or function surface rather than the feature risk.

E2E value/cost: Usually absent. If there is a smoke check, it may only prove the app starts or a route returns 200.

Clean-state confidence: Some evidence exists, but it may be hard to know whether the evidence proves the feature or only proves the app did not crash.

Typical signals:

- command output exists
- runtime path is missing or too shallow
- business result, permission boundary, data invariant, or role behavior is not checked
- next Agent can see what ran, but not why it is enough

## Targeted Completion Gate

The Agent uses a small completion gate for one feature.

Possible shape:

- selected `feature_id`
- expected behavior
- targeted static/unit check
- one runtime or integration check
- explicit pass/fail rule
- short verification log

Verification target: The feature behavior is explicit enough that the Agent knows what must be proved.

Verification depth: Checks move from general project health toward the selected behavior.

E2E value/cost: E2E may still be absent or manual. This can be suitable when the feature risk is small and runtime evidence is enough.

Clean-state confidence: Better. A reviewer can see the feature, checks, result, and pass/fail rule, but a next Agent may still need context about repo state or remaining work.

Typical signals:

- fewer unsupported completion claims
- evidence is tied to one feature
- failures are easier to interpret
- missing E2E is a conscious tradeoff, not an accident

## Minimal Real-Path Verification

The Agent adds one smallest useful E2E or system path.

Possible shape:

- completion gate
- runtime/integration check
- minimal E2E through a real route, API, page, role, or data path
- expected result and actual result
- relevant invariant check
- failure message with next safe action

Verification target: The target behavior is connected to a real user or system path.

Verification depth: Enough to test the feature where it matters, without trying to cover the whole application.

E2E value/cost: High value if the E2E catches risks that unit or route checks miss. Cost should stay low enough that it can be rerun and reviewed.

Clean-state confidence: Stronger. A next Agent can see what path was exercised, what data or role was used, and why the conclusion is justified.

Typical signals:

- route 200 is not treated as enough
- result content, permission, data state, or invariant is checked
- E2E steps are small and replayable
- failure output tells the next Agent where to look

## Handoff-Ready Completion System

The Agent uses gate, E2E, clean-state check, and handoff report together.

Possible shape:

- `completion_gate.md`
- `completion_gate.json`
- `verification_logs/<feature_id>_gate_result.md`
- `verification_logs/<feature_id>_e2e_result.md`
- `session_exit_checklist.md`
- `handoff_report.md`
- clear failure message format

Verification target: The feature, finish condition, and evidence paths are explicit.

Verification depth: Static/unit, runtime/integration, and minimal real-path evidence are all connected to the selected feature.

E2E value/cost: E2E is part of the closing decision, but still scoped to the smallest meaningful path.

Clean-state confidence: High. A next Agent should be able to judge state, evidence, failures, and next action from repository files.

Typical signals:

- completion is no longer just the execution Agent's claim
- passing depends on evidence paths
- failed checks keep the feature `active` or `blocked`
- handoff reduces oral supplementation

## Strict Independent-Close System

The learner builds a serious high-structure Unit4 completion system. This version should be accurate and plausible, not intentionally bad.

Possible shape:

- handoff-ready completion system
- scripted verification command
- required command output saved in logs
- next-Agent handoff drill
- independent evaluator review
- clean-state checklist that checks temporary files, stale notes, unrelated diff, evidence links, and next safe task
- comparison report that explains what should stay, relax, merge, or be removed

Verification target: The target behavior, non-goals, completion rule, and disallowed closure conditions are explicit.

Verification depth: The system requires proof across static/unit, runtime/integration, and minimal E2E evidence before `passing`.

E2E value/cost: E2E must prove a real path and the key invariant. The risk is that E2E or scripts become too hard to run, too broad, or too brittle.

Clean-state confidence: Very high when done well. A new Agent and independent evaluator can inspect the repo and decide whether completion is justified.

Possible new problems:

- verification becomes slower than the feature warrants
- E2E covers too much and fails for unrelated reasons
- scripts are brittle or environment-specific
- logs become long but not more reviewable
- clean-state checks become ritual instead of evidence
- handoff repeats the same information in several places
- students mistake more artifacts for stronger completion

Use this version as the serious "too much completion structure" experiment. If it improves proof and handoff, keep the parts that caused the improvement. If it creates noise, delay, or fragile checks, merge, relax, or remove the parts that did not change Agent behavior.

## Choosing A Suitable Completion System

The final Unit4 system may be simpler than the strict version.

A suitable design should answer:

- What exact behavior must be proved?
- What evidence is enough for this repo and feature?
- Is a minimal E2E necessary, and what should it prove?
- What failure message helps the next Agent act safely?
- What clean-state checks prevent false closure?
- What handoff information must stay separate?
- Which artifacts add burden without changing Agent behavior?

Do not score by artifact quantity.

Score whether the final completion system makes `passing` more evidence-grounded and handoff-ready than the light baseline, without keeping unnecessary verification burden from the strict version.
