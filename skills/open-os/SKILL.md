---
name: open-os
description: Use when the user says "open os", "Open OS", "开放作业体系", or asks to use a probe flow before development, debugging, refactoring, audits, DSL work, Comdr work, or Cocos work.
---

# Open OS

## Rule

Development starts with a probe flow: gather direct evidence, define success, then change files.

Do not implement while the target, owner boundary, or success proof is still guessed.

## Probe Flow

Before editing, identify the smallest useful set of probes:

1. State probe: what is true now? Use source reads, `rg`, git diff, logs, build output, screenshots, runtime checks, Comdr probes, schemas, or existing tests.
2. Boundary probe: which file, component, command, data path, document, cache, generated artifact, or runtime layer owns the behavior?
3. Success probe: what exact command, output, UI state, file diff, test, or audit result proves the work is done?
4. Drift probe: what stale doc, old eval, cache, duplicate definition, generated file, or partial path could make a false pass?
5. Audit probe: after the change, what source truth must be reread to prove code, tests, docs, and cleanup agree?

Keep probes practical. Use only the probes needed to remove guessing.

## Work Gate

Start implementation only after these are clear enough:

- goal
- owner boundary
- success proof
- verification command or manual check
- drift or cleanup risk

If any item is unclear, inspect more or ask.

## Fix Rule

Fix the owner cause, not only the visible symptom.

If the same class of failure appears twice, stop patching and run a root-cause loop:

- reread the source truth
- explain the cause
- check stale data, caches, generated files, docs, and runtime boundaries
- change the owner area
- verify again

## Cleanup Rule

This project is not online yet. Refactor or delete stale structure when it makes the system clearer, but finish the related cleanup:

- This is a refactor-phase project: do not keep old compatibility paths, legacy aliases, or dual implementations unless the user explicitly requires migration compatibility.
- remove dead paths and duplicate definitions
- update docs, tests, scripts, evals, configs, or generated artifacts that belong to the change
- Treat documentation as project assets: when behavior, design, commands, contracts, or ownership boundaries change, update the relevant docs in the same delivery.
- verify UTF-8 when touching Chinese text, Markdown, JSON, configs, scripts, or generated files

## Output

At the start of an Open OS task, output only:

- Goal
- Probe Flow
- Success Criteria
- Verification
- Audit
- Blockers

Keep it short. The brief is a launch checklist, not a report.
