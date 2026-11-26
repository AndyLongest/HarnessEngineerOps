<!-- Intent: Preserve the reusable task-design method with general examples. Updated: 2026-11-26. Sources: 4c417d4, ed902d3. -->
# Reflection-Eliciting Tasks Workflow

Intent: This note records a reusable design workflow for course units. It turns one unit idea into a Reflection-Eliciting Task without copying another unit's artifacts or giving students a fixed answer.

## Core Teaching Pattern

The course should use Reflection-Eliciting Tasks, not recipes.

Each unit should let learners compare:

- under-structured work: the Agent moves fast but guesses, drifts, misses risk, or produces weak evidence
- sophisticated high-structure work: the Agent gets stronger guidance, but the structure may become slow, noisy, brittle, or hard to review
- suitable work: the learner keeps the structure that improves Agent behavior and removes or relaxes the parts that only add burden

The final answer should stay open-ended. Learners must justify why their chosen design fits the repo, task, risk level, and evidence from the runs.

## General Workflow

### 1. Identify The Learning Lenses

Before writing levels or instructions, identify the small set of ideas students must practice throughout the unit.

Examples:

- Repository guidance: cold start, evidence access, Agent attention, human review burden
- Execution control: task decomposition, finish definition, complexity control, safety-efficiency tradeoff
- Completion and handoff: verification target, verification depth, E2E value/cost, clean-state confidence

These lenses should appear at every level of the unit. Higher levels should make the same lenses more explicit, more fine-grained, or stricter.

### 2. Name The Reflection Tension

State the tension students must learn to judge.

Examples:

- Repository guidance: documentation too thin vs documentation too detailed
- Execution control: task, finish, scope, permission, and trace control too loose vs too tight
- Completion and handoff: verification too light vs verification too heavy

The unit should not begin with a best-practice checklist. It should begin with the judgment problem.

### 3. Build A Reference Ladder

Create a reference file that shows increasing levels of structure.

The ladder should not list unrelated options. Each level should express the same learning lenses with increasing explicitness, granularity, and strictness.

Good reference levels:

- show what is controlled at that level
- show what Agent behavior may improve
- show what new burden or failure may appear
- avoid declaring one level as the standard answer

The highest level should match the sophisticated test case for the unit. It should be accurate and plausible, not intentionally bad.

### 4. Test The Under-Structured Version

Ask learners to run the task with insufficient support.

The goal is to show what the repo or workflow fails to communicate by itself.

Learners should infer:

- Which Agent abilities are weak or missing?
- Which failures come from missing guidance, boundaries, or evidence?
- What oral explanation did the learner feel tempted to give?
- What did the Agent do naturally when not guided?
- How did each learning lens appear in the failure?

This step should produce concrete failure signals, not a generic conclusion like "add more process."

### 5. Test The Sophisticated High-Structure Version

Ask learners to build or use a serious high-structure version that matches the top reference level.

It should be strong enough to create real improvements and heavy enough to reveal cost.

Learners should infer:

- Which Agent abilities improved?
- Which original mistakes disappeared?
- Which mistakes remained?
- Which parts changed Agent behavior in a useful way?
- Which parts looked complete but did not improve the result?
- What new burden appeared for the Agent, learner, reviewer, or maintainer?

This step prevents the common mistaken conclusion that the most detailed version is automatically enough.

### 6. Diagnose Improvement And Burden

Learners compare the under-structured and high-structure runs through the learning lenses.

They should ask:

- What improved because of added structure?
- What stayed weak despite added structure?
- What became slower, noisier, duplicated, brittle, stale, or hard to review?
- Which controls or documents should stay?
- Which should be merged, relaxed, or removed?

Do not score by artifact quantity. Score whether the learner can connect a design choice to run evidence.

### 7. Choose A Suitable Final System

Learners build or describe a final version by keeping useful structure and removing unnecessary burden.

They should not keep an artifact just because it exists. They should not remove an artifact just because minimalism sounds good.

For each important part they keep, learners should explain:

- what problem it solves
- what evidence shows the problem existed
- why it should stay separate rather than be merged
- how it improves Agent work without making human review worse

If a final retest is feasible, use the same task prompt or comparable conditions so behavior can be compared inside the same repo.

## Updating Shared Protocols

A shared protocol should translate the workflow into one unit's practice.

It should include:

- intent
- learning lenses
- under-structured run
- sophisticated high-structure run
- diagnosis of improvement and burden
- open-ended final judgment
- evidence expectations
- teacher scoring based on reasoning, not artifact count

Keep the shared protocol focused on what learners must compare and diagnose. Put optional examples or complexity levels in a reference file.

## Updating Project-Specific Guides

After the shared protocol is updated, project-specific files should only localize it.

Use the shared protocol as the structure, then adjust:

- local examples
- repo-specific failure points
- repo-specific risks
- evidence paths
- wording that conflicts with the new protocol

Project files should make the shared protocol concrete, not add another workflow layer.

For student markdown, do not refer to files outside the project folder when students may not have those files. Add the needed information directly.

## Notice Points For Future Units

### Keep The Answer Open-Ended

Do not provide a standard final complexity level for each repo.

The same repo may need different structure depending on the task, risk, and learner goal. The assignment should reward diagnosis and justification, not matching a predefined shape.

### Avoid Concept Staircases

Do not make level 1 teach one concept, level 2 teach another concept, and level 3 teach a third concept.

Every level should contain the unit's core learning lenses. The levels differ by tightness, granularity, and strictness.

### Avoid Strawman Extremes

The high-structure version must not be intentionally false or silly.

If it contains fake facts, students only learn that wrong guidance is bad. The stronger lesson is that even accurate structure can become costly when it is too broad, duplicated, stale, brittle, or hard to maintain.

### Ask About Ability Change

Diagnosis questions should focus on changes in Agent ability.

Prefer:

- What became more accurate?
- What unsafe behavior disappeared?
- What new issue appeared?
- Which part changed the Agent's route or decision?

Avoid questions that only inspect artifact shape without connecting to behavior.

### Keep Scaffolding Light

Too many tables and worksheets become another kind of over-structure.

Use a few high-value prompts. Let learners write a reasoned comparison rather than filling a large form.

### Separate Reference From Protocol

Reference files can show possible levels or examples, but they should not become answer keys.

Protocol files should tell learners how to compare, diagnose, and improve. Reference files should help them imagine possible designs.

### Compare Within The Same Repo

Do not compare raw results across different repositories.

A small repo and a large repo need different amounts of structure. The meaningful comparison is within the same repo before and after the comparison runs.

### Preserve Evidence Orientation

The final design should help the Agent reach evidence, not replace evidence.

For any unit, watch for artifacts that make the Agent confident without making it better grounded.

## Principle

Structure should be earned.

Add structure when the Agent lacks guidance, boundaries, or evidence. Remove or relax structure when it creates noise, delay, duplicated responsibility, or review burden.
