# Assessment Profile Contract

An assessment profile defines what the skill may claim about a learner in a specific course, unit, or task. It may be a rubric, a concise Markdown profile, or structured data, provided the required fields are explicit.

## Required Fields

| Field | Requirement |
|---|---|
| Assessment scope | Name the course, unit, task, or learner activity being assessed. |
| Target constructs | Name each construct and provide an operational definition. |
| Task knowledge | State the taught knowledge, method, or task requirements relevant to the assessment. |
| Evidence threshold | State what counts as admissible evidence and what does not for each construct. |
| Attribution boundary | State how assignment scaffolds, Agent-generated material, and learner evaluation affect the claims. The core attribution rules apply if no stricter rule is supplied. |
| Reporting rule | State whether results are evidence-strength claims only or include rubric scores, and whether any constructs must remain separate. |

## Optional Fields

Add these when the assessment needs them:

- scoring items, anchors, and grade thresholds;
- required and optional deliverables;
- assignment brief and starter prompts;
- modality hypotheses or exclusions;
- performance constructs that must be reported separately from learner constructs;
- calibration examples, counterexamples, or teacher decisions.

## Default Interaction

When a submission is available but the profile is missing or cannot identify the target constructs, ask for:

```text
Please provide the assessment profile or rubric for this task. It needs the target constructs, the relevant task knowledge, what counts as evidence, and whether you want evidence-strength claims, rubric scores, or both.
```

Do not infer a course-specific profile from filenames, polished reflections, or the structure of a submission. Once a usable profile is supplied, inspect sessions first and then select supplementary output and reflection dimensions through qualitative analysis.
