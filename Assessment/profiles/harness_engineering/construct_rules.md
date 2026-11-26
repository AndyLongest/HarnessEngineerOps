# Episode and Construct Coding Rules

## A. Decision/adaptation episode schema

A useful episode may include:

1. `goal_or_prior_state`
2. `trigger_or_evidence`
3. `recognition`
4. `diagnosis_or_evaluation`
5. `change_or_decision`
6. `verification_or_follow_up`
7. `attribution`
8. `opportunity`

Do not require all fields to be present. Missing fields are informative.

---

# B. K — Applied Domain Knowledge

## Strong indicators

- Learner diagnoses a real task using a taught domain concept and the diagnosis fits available evidence.
- Learner selects an appropriate method and applies it to a concrete object.
- Learner modifies a generic method to fit the task while preserving its core rationale.
- Learner verifies whether the method solved the identified problem.

## Weak/non-indicators

- Naming concepts without application.
- Copying a template without task-specific decisions.
- Agent applies the correct method autonomously.
- Reflection says “I learned X” without observable use.

## Scaffold rule

Correct use of a supplied template can support K because application of learned knowledge may be scaffolded. Qualify independence if the learner did not make visible task-specific choices.

---

# C. M — Hybrid Metacognitive Regulation

Code four subcomponents separately. These M1-M4 definitions and evidence thresholds apply across Harness Engineering tasks. Taught knowledge and task conditions determine what regulation concerns and whether an opportunity exists. Select applicable constructs by modality using [the core evidence model](../../session_evidence/references/evidence_model.md).

## M1 Planning

Evidence includes:

- identifies the real current objective;
- establishes task-specific success evidence;
- anticipates likely uncertainty or risk;
- decides what context/resources/verification are needed;
- changes plan when initial assumptions are insufficient.

Compare the candidate planning text with assignment instructions and starter prompts. Rote reproduction alone does not establish learner M1. Credit observable task-specific adaptation or evaluation under the same planning criteria, even when the task itself is scaffolded. A request appearing before Agent action does not by itself establish that the learner designed the plan.

## M2 Monitoring

Evidence includes:

- notices discrepancy between goal and current state;
- recognizes incomplete evidence;
- notices that Agent behavior, scope, assumptions, or state diverged;
- tracks whether an intervention is actually working.

A test failure by itself is not learner monitoring. The learner must visibly notice/use the signal.

## M3 Evaluation / Calibration

Evidence includes:

- compares Agent confidence/claim with independent evidence;
- identifies uncertainty or insufficiency of available evidence;
- revises trust based on success/failure history;
- distinguishes “code written” from “verified complete”;
- chooses verification intensity based on risk/evidence.

Simply distrusting the Agent is not calibration. Calibration requires evidence-sensitive adjustment.

## M4 Adaptive Regulation

Evidence includes learner-driven change to one or more of:

- task framing or scope;
- context supplied;
- verification strategy;
- tool/permission boundary;
- human–AI division of labor;
- harness/control mechanism;
- sequencing or stopping rule.

Retries without a meaningful strategic change are not adaptive regulation.

## Full reactive episode

Strong M evidence often has:

`signal -> learner recognizes -> learner evaluates/diagnoses -> learner changes strategy -> learner checks consequence`

## Proactive M

A failure does not need to occur. Proactive M is supported when the learner:

`anticipates a task-specific risk -> explains why it matters here -> installs a preventive control -> defines what evidence would make them revise/relax it`

A generic prewritten safeguard with no task-specific judgment is primarily K/procedural evidence.

---

# D. R — Conditional Professional Judgment

R asks whether the learner has conditionalized a professional decision.

## Core structure

`decision/method + conditions + rationale/mechanism + boundary/exception/revision trigger`

Not every strong R episode must literally use those four labels, but the substance should be recoverable.

## Examples of stronger evidence

- “WIP=1 is appropriate for this coupled feature because verification interactions are expensive; I would relax it for independent documentation changes with separate gates.”
- “This database migration needs human approval because rollback is costly; read-only queries do not need the same gate.”

## Weaker evidence

- “Use WIP=1.”
- “Humans should review risky operations.”
- A compliant diff with no visible rationale or boundary condition.

## Relation to supplied rubric R items

If the course already has R items (e.g., scope restraint, proportionality), preserve those scores. Behavior-focused R items provide evidence of judgment-in-action but may not by themselves establish the full conditional rationale. Explain this in the personal analysis rather than inventing a duplicate CPJ score.

---

# E. I — Prospective Insight

## Core chain

`current observation -> mechanism -> transferable principle -> future test/boundary condition`

## Strong evidence

The learner identifies what future evidence would make the proposed principle valid, invalid, stronger, or obsolete.

## Weak evidence

- future tool shopping;
- “next time I will add more tests”;
- repeating later-unit terminology;
- predictions with no link to current evidence.

---

Use the general [episode and attribution rules](../../session_evidence/references/episode_and_attribution_rules.md) for learner attribution and opportunity coding.
