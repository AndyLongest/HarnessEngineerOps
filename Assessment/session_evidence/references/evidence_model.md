# Evidence Model

## 1. Unit of analysis

The assessment target is the **individual learner**, but evidence is generated inside a human–AI–tool–task system. Therefore every claim must preserve:

`source -> actor -> event/episode -> task condition -> construct -> claim`

Never collapse system behavior directly into learner ability.

## 2. Evidence item

A minimally useful evidence item contains:

- `evidence_id`
- `source_path`
- `source_type`
- `task_or_phase`
- `timestamp_or_location`
- `actor/content_type`
- `observable_content_summary`
- `provenance`
- `dependency_parent` when derivative

## 3. Provenance and independence

### Primary/contemporaneous

Session text/actions created during the task, tool outputs, direct diffs, direct test output.

### Primary/artifact

A concrete product or control artifact whose existence/content can be inspected.

### Retrospective

Reflection or after-action explanation. It can clarify retrospective judgment or insight, but is weaker for proving contemporaneous regulation.

### Derivative

A report or reflection generated from another source, including Agent-written prose later submitted unchanged.

### Automated evaluation

Evaluator output. Useful as a scoped judgment, not as ground truth.

## 4. Source dependence rule

Two sources are not independent merely because they are separate files.

Examples of dependence:

- identical text;
- one file explicitly summarizes another;
- Agent writes a reflection that later appears as the submitted reflection;
- evaluator output quotes the same underlying test run.

Confidence should increase only with *independent* evidence or evidence that adds a genuinely different observational channel.

## 5. Coverage

For each session/source, record:

- full / partial / reconstructed / unknown;
- start and end phase if inferable;
- whether tool outputs were removed;
- whether learner turns are preserved;
- whether timestamps are reliable.

Absence in a partial or reconstructed source must be worded as `not visible in the supplied record`, not `did not occur`.

## 6. Contradiction handling

Agent sessions anchor the learner assessment across the constructs selected by the supplied profile. This priority concerns the assessment workflow, not unconditional evidential authority. Do not resolve contradictions by majority vote. Prefer the source closest to the behavior being claimed, accounting for coverage and attribution.

Example:

- Reflection: “I verified the user flow.”
- Test log: only static checks were run.

Report: `The reflection claims user-flow verification, but the submitted execution evidence only establishes static checks; system-level verification is not established.`

## 7. Coursework vs ability

A coursework rubric evaluates whether a required demonstration was submitted. Ability inference evaluates what the evidence justifies saying about the learner.

Possible combination:

- Rubric score: low because required trace is absent.
- Ability claim: `The profile construct is not established from the available record`, not `low ability`.

## 8. Performance boundary

Successful output can contextualize a profile construct but does not prove learner attribution.

Conversely, high-quality regulation can be demonstrated in a blocked or unsuccessful task.

Keep system-performance conclusions separate from individual-ability conclusions.

## 9. Qualitative modality selection

Keep task/profile selection and evidence-modality selection separate. The supplied profile defines the constructs and their task-specific knowledge points. Each modality selectively informs the same profile constructs.

Begin with qualitative analysis of the relevant sessions to establish provisional claims for the profile's constructs. For each supplementary artifact or reflection, inspect the actual content before selecting dimensions. Record:

- source and evidence locators;
- content summary or open codes;
- selected constructs and the reason each is observable;
- constructs with no clear opportunity or unknown coverage;
- admissible evidence, actor attribution, and source dependencies.

An applicable dimension with insufficient evidence is `not established`. A dimension without an observation opportunity is `not observable`; a partial export may instead leave opportunity unknown. None implies low ability.

An artifact may demonstrate correct knowledge application at output level while learner attribution remains unresolved. A reflection may articulate a judgment without proving it occurred during execution. Profiles may provide task-specific modality hypotheses, but qualitative analysis must confirm or revise them for each source.

## 10. Session-led cross-modality triangulation

For each claim, retain the provisional session conclusion, the supplementary evidence and its relation to that claim, and the final conclusion with a reason for any change.

| Relation | Effect on assessment |
|---|---|
| Independent corroboration | Strengthen confidence when attribution and construct match |
| Complementary evidence | Fill a specific gap, such as decision rationale or the resulting artifact; preserve what each source establishes |
| Contradiction | Re-examine scope, chronology, attribution, and source quality; qualify or revise the claim, or retain the conflict |
| Derivative repetition | Link to the originating evidence; no additional independent confirmation |
| No relevant evidence | Leave the session claim unchanged; do not penalize an unsuitable modality |

For example, a session shows a learner selecting a boundary, an output confirms its implementation, and a reflection explains its conditions. Together they may support a stronger profile-defined judgment claim. If the Agent generated all three, their agreement does not establish learner judgment. If a reflection asserts end-to-end verification but available logs show only static checks, retain the evidence limit rather than increasing confidence.

Supplementary evidence can introduce a claim absent from a partial session; label it supplementary-only until behavior is corroborated. When no usable session exists, perform the available qualitative analysis and report its coverage and attribution limits. Do not invent a session baseline or average modality scores. Report each profile construct separately.
