<!-- Intent: Record the provenance and packaging of the general assessment contribution. Updated: 2026-11-26. Upstream base: 2396734. -->
# Assessment contribution record

This package adapts linmou's course-design and assessment work into general principles for evaluating harness tradeoffs and learner evidence.

| Released material | Source |
|---|---|
| Tradeoff-design principles | Lifecycle tradeoff matrix and Reflection-Eliciting Tasks workflow; source commits `6834912`, `4c417d4`, `d4be79f`, `ed902d3` |
| Reflection-Eliciting Tasks workflow | `reflection_eliciting_tasks_workflow_v0531.md`; examples generalized to documentation, control, and verification tasks |
| K/M/R/I profile and construct rules | HarnessCourseOps working-tree assessment reorganization; profile adapted for task-supplied knowledge and evidence-strength reporting |
| Session evidence skill and references | `linmou/ai-augmented-expertise-assessment` commit `00e3b29ab329855705d9f044f16a246418c767b8`; six original files |

The profile links task requirements and construct definitions to the original skill's profile, evidence, attribution, and reporting contracts. Course-specific numeric scoring belongs in a separately supplied task rubric.

## Validation

On 2026-11-26, all 12 added Markdown files passed relative-link and fenced-block checks. The six bundled skill files matched the pinned upstream commit byte for byte. `git diff --cached --check` passed. Profile review checked construct definitions, task-knowledge binding, evidence thresholds, attribution, and reporting against the bundled profile contract. These checks establish package integrity and documentation consistency; reliability or learning-effect claims require their own empirical evidence.
