# Documentation System Complexity Reference v0531

Intent: This file gives learners examples of documentation-system complexity. These levels are reference points only, not standard answers and not required final designs.

## Existing Repo Only

No new Harness docs. The Agent uses existing README files, source files, config files, and repository structure.

This is useful as the first test because it shows what the repository communicates by itself.

## Root Entry Only

One root `AGENTS.md` gives purpose, first files to inspect, startup hints if known, and major risks.

This can be enough for a small repo when the source layout is obvious.

## Root Entry Plus Run And Risk Notes

The repo has a root entry plus a startup path and risk guidance, either as separate files or as sections in the root file.

Possible files:

- `AGENTS.md`
- `RUNBOOK.md` or a startup section
- `KNOWN_RISKS.md` or a risk section

This can help when the Agent understands the domain but misses how to run the project or what not to touch.

## Root Entry Plus Scope

The repo has a root entry, startup/risk guidance, and a scope note that says what is in and out of the current handoff.

Possible files:

- `AGENTS.md`
- `scope_contract.md`
- `RUNBOOK.md`
- `KNOWN_RISKS.md`

This can help when the repo has noisy folders, generated files, static/vendor assets, or multiple possible work areas.

## Task-Oriented Topic Docs

The repo has a small number of topic docs tied to real cold-start failures.

Possible files:

- `ROLE_FLOW.md`
- `DATA_MODEL.md`
- `PROJECT_MAP.md`
- `API_FLOW.md`
- `TRANSFER_RULES.md`

Only add these when the Agent's logs show that the topic is hard to infer from the root entry and source files alone.

## Detailed Hierarchical Doc System

The repo has root guidance plus nested docs by topic, role, workflow, or module.

Possible shape:

- root `AGENTS.md`
- `docs/README.md`
- setup docs
- architecture docs
- workflow docs
- module-specific docs
- risk docs
- route/data/model maps
- role-specific docs

This can be useful for complex repositories, but it can also create duplicate facts, stale guidance, slow cold-start behavior, and review burden. Use it as an experiment and keep only the parts that prove useful for this repo.
