# ACTIVE WORK HANDOFF — TLTD

## Synchronization state
- Last updated: `2026-09-17`.
- Memory repository: `huycodedie/Ai_MEMORY_TLTD`.
- Branch: `main`.
- Last completed authority commit before this handoff: `b5b0838ee471c9fdd79703d46000ce9db6f36570` — `docs(ui): lock responsive layout direction`.
- This file must be updated with the final commit SHA after each subsequent accepted handoff change.

## Current milestone state
- `UI-02 = LOCKED` as of `2026-09-17`.
- `UI-POLISH-01 Phase A = AUDIT COMPLETE`.
- `UI-POLISH-01 = RESPONSIVE LAYOUT DESIGN REQUIRED / IMPLEMENTATION NOT STARTED / NOT LOCKED`.
- `P08 = NOT STARTED`.

## Current active objective
Design the responsive portrait UI layout and information hierarchy before broad Unity UI implementation.

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
7. `PROJECT_MEMORY/DESIGN_CHANGELOG.md`

## Role model
- ChatGPT/Codex: primary coordinator, Tech Lead, design authority and memory publisher.
- Antigravity: secondary Unity implementation/test executor.
- GitHub `main`: persistent canonical memory source.

## Known blockers
- None for responsive layout design.
- Unity implementation remains intentionally blocked until the layout specification/wireframe is reviewed.
