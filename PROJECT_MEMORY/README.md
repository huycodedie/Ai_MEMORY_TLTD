# TLTD PROJECT_MEMORY

## Purpose

This directory is the AI-readable local memory package for the Unity project `E:\code\TLTD`.

The repository `huycodedie/Ai_MEMORY_TLTD` branch `main` is the persistent canonical memory source. Google Antigravity should synchronize and consume a LOCAL copy inside the TLTD project.

## First-time installation into TLTD

If `E:\code\TLTD\PROJECT_MEMORY` does not exist, obtain this repository and copy its contents into that directory.

If the user does not want the whole memory repository nested inside the game repository, copy only the Markdown files from this directory plus the referenced D/P documents into `E:\code\TLTD\PROJECT_MEMORY`.

## Operating rule

After a new design decision is explicitly LOCKED:

1. Update the memory source in GitHub.
2. Sync the local `PROJECT_MEMORY` copy.
3. Antigravity reads local files before implementation.
4. Code and tests are then updated.
5. Acceptance evidence is recorded before the milestone is marked LOCKED.

Every approved decision must also follow `CONTINUITY_AND_SYNC_AUTHORITY.md`: update the active handoff, commit, push and verify the remote state. Conversation history alone is not durable project memory.

## Mandatory continuation entrypoint

For a new chat, changed workspace or resumed task, read in this order:

1. `AI_RULES.md`
2. `CONTINUITY_AND_SYNC_AUTHORITY.md`
3. `ACTIVE_WORK_HANDOFF.md`
4. `CURRENT_DESIGN_AUTHORITY.md`
5. `DESIGN_CHANGELOG.md`
6. Authority and evidence files referenced by the active handoff

## Do not treat this folder as gameplay code

This directory is a contract/memory layer. It does not itself prove that the Unity implementation is correct.

Implementation evidence must come from the actual project, tests, Unity Play Mode, regression logs, and visual checks where applicable.

## Current UI layout authority

Before implementing new UI layout work, read:

- `UI_DESIGN_AUTHORITY.md` — global shell and system-screen structure.
- `UI_RESPONSIVE_LAYOUT_AUTHORITY.md` — responsive portrait rules, Safe Area coverage, reference-resolution meaning, visual-reference boundary and the required layout-first implementation order.
- `UI-POLISH-01_ARCHITECTURE_AUDIT.md` — current modal/lifecycle architecture findings.
- `UI-POLISH-01_PHASE_B1_TECH_LEAD_REVIEW.md` — review of the out-of-sequence local B1 implementation and requirements before acceptance.
- `UI-POLISH-01_RESPONSIVE_LAYOUT_SPEC.md` — locked Project Owner-approved responsive shell, screen and modal layout authority.
- `UI-POLISH-01_PHASE_B1_SOURCE_REVIEW_TASK.md` — exact read-only Antigravity task for actual B1 source and evidence inspection.
