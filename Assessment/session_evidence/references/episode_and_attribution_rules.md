# Episode and Attribution Rules

## Decision and adaptation episode

A useful episode may include:

1. `goal_or_prior_state`
2. `trigger_or_evidence`
3. `recognition`
4. `diagnosis_or_evaluation`
5. `change_or_decision`
6. `verification_or_follow_up`
7. `attribution`
8. `opportunity`

Do not require every field. Preserve missing fields rather than inferring them.

## Attribution

Use one primary attribution label for each construct-relevant event or episode:

- `learner_initiated`: the learner introduces the relevant goal, diagnosis, concern, strategy, judgment, or revision.
- `agent_proposed_learner_evaluated`: the Agent proposes an idea and the learner critiques, modifies, rejects, or conditionally accepts it with task-specific reasoning.
- `agent_proposed_learner_accepted`: the Agent proposes an idea and learner acceptance is visible without substantive evaluation.
- `teacher_or_assignment_scaffolded`: the action is prescribed by supplied teaching or task materials.
- `agent_led`: the Agent generates and executes the substantive reasoning or decision.
- `harness_or_tool_automatic`: the behavior occurs automatically through a tool, hook, evaluator, test, or workflow mechanism.
- `mixed_or_unclear`: the source cannot support a confident separation.

Inspect a `user` role message before assigning learner attribution. Tool results, imported context, IDE selections, hooks, and coordinator prompts are not learner claims. Compare apparent learner plans against supplied assignment prompts and templates before treating them as learner-originated.

## Opportunity

For each selected construct, record one opportunity status:

- `direct_opportunity`: the source visibly creates a situation in which the construct could be demonstrated.
- `proactive_opportunity`: the learner anticipates and manages a task-specific risk before failure occurs.
- `no_clear_opportunity`: the source contains no relevant decision, perturbation, or proactive reasoning.
- `opportunity_unknown_due_to_coverage`: partial or reconstructed evidence prevents deciding whether an opportunity occurred.

Do not convert `no_clear_opportunity` or `opportunity_unknown_due_to_coverage` into a claim of low ability.
