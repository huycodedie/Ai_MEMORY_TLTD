# TLTD PROJECT_MEMORY

## Purpose

This directory is the AI-readable local memory package for the Unity project `E:\code\TLTD`.

The repository `huycodedie/Ai_MEMORY_TLTD` is the long-term backup. Google Antigravity should consume a LOCAL copy inside the TLTD project.

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

## Do not treat this folder as gameplay code

This directory is a contract/memory layer. It does not itself prove that the Unity implementation is correct.

Implementation evidence must come from the actual project, tests, Unity Play Mode, regression logs, and visual checks where applicable.

## Current UI layout authority

Before implementing new UI layout work, read:

- `UI_DESIGN_AUTHORITY.md` — global shell and system-screen structure.
- `UI_RESPONSIVE_LAYOUT_AUTHORITY.md` — responsive portrait rules, Safe Area coverage, reference-resolution meaning, visual-reference boundary and the required layout-first implementation order.
- `UI-POLISH-01_ARCHITECTURE_AUDIT.md` — current modal/lifecycle architecture findings.
