# CURRENT DESIGN AUTHORITY — TLTD

## Purpose
This file is the quick-reference authority for the **current** design state. It does not erase historical D documents. Historical rules remain traceable through `D1_D23_LOCKED.md`, amendment files, and `DESIGN_CHANGELOG.md`.

## Authority order
1. Original user-approved D1-D23 decisions.
2. Later explicit user-approved amendments/revisions that supersede an older rule.
3. P01+ behavior that was actually tested and explicitly accepted/locked by the user.
4. Current implementation evidence.
5. New proposals.
6. General AI assumptions.

If a conflict cannot be proven as superseded: STOP and report it. Never guess.

## Current locked amendments
### Combat resource / Bun
- Bun applies to Normal Monster Battle.
- 1 Bun = 1 Hero combat action.
- Hero and Companions both stop when Bun reaches 0 during Normal Battle.
- Boss Battle does not depend on Bun.

### Chest / Drop Level
- `Chest Level = Drop Level = Cấp Rơi`.
- One concept, one runtime authority.

### Item Level
- Item Level is based on current Hero Level.
- `abs(ItemLevel - HeroLevel) <= 5`.
- Distribution inside ±5 is TBD unless explicitly sourced.

### Rarity / Quality
- Cấp Rơi controls availability/unlock and probability of qualities.
- The nine qualities visible in the reference UI are not the maximum.
- Higher qualities may exist.
- `0%` at a lower Cấp Rơi can mean unavailable/not unlocked; it does not mean the quality does not exist.
- Rarity count, names beyond sourced data, unlock thresholds and probabilities remain data-driven/TBD unless explicitly locked.
- Never hard-code `Tối Thượng` as the final rarity.

### Equipment
- 12 wearable equipment slots are locked.
- Current concepts: Vũ khí/Kiếm, Mũ, Khăn che mặt, Áo, Quần, Giày, Găng tay, Đai lưng, Áo choàng, Dây chuyền, Nhẫn, Bùa/Ngọc.
- Do not use `SPECIAL` as a player-facing slot name.

### Attack interval
- Hero: 1.5s baseline.
- Companion: 2.0s baseline.
- Both remain configurable and independent.

### Companion combat
- Companion uses the common Combat Resolver/pipeline.
- Combo/Counter must not have a separate Companion engine.
- Companion has HP, can die and respawn; this supersedes older historical text that described Pets/satellites as having no HP.

### Recycle
- Equipment recycle returns GOLD ONLY.
- Base Auto-Recycle rule: lower item CP than the currently equipped item is eligible.
- Future Preferred Attribute/Affix protection can keep an otherwise eligible item.

### Chest upgrade
- One level at a time; no queue; no auto-chain; no cancel; no claim button.
- During upgrade, opening uses the currently completed level.
- At persisted `CurrentTime >= FinishTime`, auto-complete to the next level and enter IDLE.
- Persist timestamps; do not rely on transient timers for authority.

## UI structure baseline
- The game is a **2D mobile portrait / vertical-screen game**.
- The bottom navigation is a **global game shell**, not part of an individual system screen.
- There are **5 primary global navigation positions**.
- The **center position is the Main Hub / Main Game Frame**.
- Major systems replace the Main Content Area above the navigation; they do not create a second navigation framework.
- **Công Pháp is a dedicated system screen/module**, not another tab inside a generic all-purpose function panel.
- Công Pháp may contain its own overview, category list, and detail sub-screens while retaining the global 5-position navigation shell.
- Exact navigation labels/icons, portrait resolution, pixel layout, visual art and detailed interaction remain TBD unless separately approved.
- Full structural rules are recorded in `PROJECT_MEMORY/UI_DESIGN_AUTHORITY.md`.

## P07.8 status
P07.8 Shield/Barrier is LOCKED according to the latest user-provided acceptance report: Automated 55/55, Play Mode 35/35, UI 5/5, Visual V01-V08 PASS, Master Regression P01-P07.8 PASS.

## P07.9 status
P07.9 is in active implementation/audit and is **not locked**. Approved design decisions include:
- Stun interrupts active Cast/Channel.
- Freeze interrupts active Cast/Channel.
- Root does not interrupt.
- Ordinary damage does not interrupt.
- Rage is consumed at Cast Start; interrupted casts receive no Rage refund.
- Interrupted before completion has no cooldown.
- Interrupted cast does not execute deferred final effects; already-executed channel ticks remain.
- Existing EntityStatusController remains the sole CC authority.
- Existing Entity.InterruptCurrentAction is the integration point.
- No second skill execution authority, global loop, coroutine, async loop, or Animator-dependent timing system.

## Implementation rule
P01+ tested-and-accepted behavior may supersede an older historical design rule. Record the change; do not silently overwrite history.
