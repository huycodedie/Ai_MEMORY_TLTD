# ACTIVE WORK HANDOFF — TLTD

## Synchronization state
- Last updated: `2026-09-17`.
- Memory repository: `huycodedie/Ai_MEMORY_TLTD`.
- Branch: `main`.
- Authority base verified before this handoff update: `fd5b3e57720649f2e62973dec46aef0b627d9972` — `docs(ui-polish-01): record b1 review gate`.
- The latest remote commit must always be verified after publication; a handoff file cannot embed the SHA of the commit that contains itself.

## Current milestone state
- `UI-02 = LOCKED` as of `2026-09-17`.
- `UI-POLISH-01 Phase A = AUDIT COMPLETE`.
- `UI-POLISH-01 Responsive Layout = LOCKED / PROJECT OWNER APPROVED` as of `2026-09-17`.
- `UI-POLISH-01 overall = NOT LOCKED`.
- `UI-POLISH-01 Phase B1 = LOCAL IMPLEMENTATION REPORTED / NOT ACCEPTED / VERIFICATION PENDING`.
- `P08 = NOT STARTED`.

## Current active objective
Perform read-only actual-source inspection of the reported local Phase B1 implementation and prepare a bounded reconciliation plan against the locked responsive layout.

`1080x1920` is the reference coordinate system only. The design must support common portrait phones, tall screens, portrait tablets, notches and gesture/home-indicator Safe Areas.

## Required next deliverable
Create and review a responsive UI layout specification/wireframe covering at minimum:

- Global portrait shell.
- Top HUD/resource region.
- Combat viewport and protected combat zone.
- Hero/Monster HUD placement.
- Skill/action region.
- Five-position Global Bottom Navigation.
- Modal layer and backdrop.
- Equipment Comparison.
- Cấp Rơi.
- Tâm Pháp/Công Pháp.
- Hero and Companion/Hiệp Khách presentation.
- Compact, standard and tall portrait behavior.
- Tablet width constraints and Safe Area behavior.

Do not allow the implementation executor to invent screen composition while writing code.

Locked authority: `PROJECT_MEMORY/UI-POLISH-01_RESPONSIVE_LAYOUT_SPEC.md`. It defines root hierarchy, Safe Area ownership, responsive classes, global shell zones, combat/system layout, modal geometry and B1 reconciliation gates.

An out-of-sequence local Phase B1 implementation has been reported. Freeze further Phase B edits, preserve the local files for inspection, and do not promote the report's `IMPLEMENTED / VERIFICATION PASS` claim into canonical status. Inspect the actual B1 source and raw evidence, then define exact reconciliation changes before authorizing any further Unity edit.

## Visual reference
Project Owner-approved layout/visual reference:

`https://drive.google.com/drive/folders/1EtN2qgqELrRvmt5JAnacgRKz4TMQV8jY`

Use the sample `Giang Hồ Trong Tay` screens for layout/composition guidance only. They do not override TLTD gameplay authority.

## Current exclusions
Do not start the following before responsive layout approval and runtime stability:

- Final visual polish.
- Decorative frames and final color treatment.
- Final icon art.
- Presentation-only transitions or tweening.
- Unity `Animator` work.
- Decorative VFX.

Functional layout, anchoring, Safe Area support, scrolling, input blocking and modal lifecycle remain required structural work.

## Mandatory reading for continuation
1. `PROJECT_MEMORY/AI_RULES.md`
2. `PROJECT_MEMORY/CONTINUITY_AND_SYNC_AUTHORITY.md`
3. `PROJECT_MEMORY/CURRENT_DESIGN_AUTHORITY.md`
4. `PROJECT_MEMORY/UI_DESIGN_AUTHORITY.md`
5. `PROJECT_MEMORY/UI_RESPONSIVE_LAYOUT_AUTHORITY.md`
6. `PROJECT_MEMORY/UI-POLISH-01_ARCHITECTURE_AUDIT.md`
7. `PROJECT_MEMORY/UI-POLISH-01_PHASE_B1_TECH_LEAD_REVIEW.md`
8. `PROJECT_MEMORY/UI-POLISH-01_RESPONSIVE_LAYOUT_SPEC.md`
9. `PROJECT_MEMORY/DESIGN_CHANGELOG.md`

## Role model
- ChatGPT/Codex: primary coordinator, Tech Lead, design authority and memory publisher.
- Antigravity: secondary Unity implementation/test executor.
- GitHub `main`: persistent canonical memory source.

## Known blockers
- No remaining blocker for responsive layout authority; it is locked.
- Further Unity edits remain blocked until B1 actual-source inspection produces an approved reconciliation scope.
- Phase B1 acceptance is blocked on actual-source inspection, raw evidence review, responsive reconciliation and rerun verification.
