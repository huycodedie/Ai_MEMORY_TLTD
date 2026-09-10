# DESIGN CHANGELOG — TLTD

Purpose: preserve why locked decisions changed without destroying historical source material.

## Status vocabulary
- `LOCKED`: current approved rule.
- `SUPERSEDED`: older rule replaced by a later approved rule.
- `IMPLEMENTED`: code exists; acceptance may still be pending.
- `TEST DISCOVERY`: behavior learned during testing; not automatically a design change.
- `TBD`: intentionally unresolved.
- `CONFLICT`: two sources disagree and no superseding decision has been proven.

## Recorded changes

### Companion HP model
- Historical descriptions in some early material treated Pets/satellites as turret-like/no HP.
- Later D11/D15 and recovered user decisions explicitly establish Companion as a CombatEntity with HP, damage/death and 25s configurable respawn.
- Status: `SUPERSEDED` for the old no-HP description; Companion-with-HP is current.

### Bun = 0 behavior
- Earlier baseline wording could imply only Hero/normal action stopping.
- Later explicit user decision: Hero STOP + Companion STOP + Monster/Normal combat STOP when Bun reaches 0.
- Boss remains independent of Bun.
- Status: `LOCKED` current rule.

### Chest Level / Drop Level
- Earlier documentation used separate terminology and caused ambiguity.
- User explicitly unified them: `Chest Level = Drop Level = Cấp Rơi`.
- Status: `LOCKED`; one runtime concept/authority.

### Item Level range
- Current rule: Item Level is derived from current Hero Level and may differ by at most 5 levels.
- Exact probability/distribution inside the ±5 range is not locked.
- Status: range `LOCKED`; distribution `TBD`.

### Rarity ceiling
- Older historical material listed a finite set of visible rarity tiers.
- User clarified the visible nine qualities are not the maximum; higher qualities may exist and can be unavailable at lower Cấp Rơi. A displayed 0% may mean locked/unavailable.
- Status: any fixed maximum-rarity interpretation is `SUPERSEDED`; rarity system is extensible/data-driven; exact total/unlock/probabilities remain `TBD` unless sourced.

### Equipment slots
- Historical D16 used provisional names including `SPECIAL`.
- Current locked concept is 12 wearable slots: Vũ khí/Kiếm, Mũ, Khăn che mặt, Áo, Quần, Giày, Găng tay, Đai lưng, Áo choàng, Dây chuyền, Nhẫn, Bùa/Ngọc.
- Status: count `LOCKED`; exact player-facing wording may be refined only with evidence.

### Recycle reward
- Historical D16 left EXP reward unresolved.
- Later explicit decision: equipment recycle returns Gold only.
- Status: `LOCKED`; no EXP.

### P01+ precedence
- Historical D12-D16 are recovery documents, not a reason to overwrite later tested behavior.
- P01+ behavior that was tested and explicitly accepted can supersede older historical descriptions.
- Status: `LOCKED operating rule`.

### P07.8 Shield visual blocker
- Initial P07.8 acceptance had a Shield UI/visual gap.
- A remediation was performed using the existing HUD/status architecture.
- Latest user-provided acceptance report states V01-V08 PASS, UI 5/5, Play Mode 35/35, Automated 55/55 and Master Regression PASS.
- Status: P07.8 `LOCKED` based on reported acceptance evidence.

## Future revision rule
Every new gameplay change must record: old rule -> evidence/reason -> new rule -> status -> affected milestone/code -> tests required. Never delete historical decisions to hide a conflict.
