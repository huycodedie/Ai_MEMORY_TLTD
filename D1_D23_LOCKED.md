# D1-D23 LOCKED DESIGN CONTRACT

## Purpose
This file declares D1-D23 as the locked game-design contract for TLTD. The original D1-D23 document supplied by the user is the authoritative source and must be preserved verbatim when available.

## Critical preservation rule
Do NOT reconstruct missing D1-D20 from AI memory or general game-design assumptions. Do NOT silently alter D1-D23. If the original D1-D23 source is supplied later, replace/extend this index with the exact original content only after preserving it as the canonical source.

## Confirmed locked decisions available in current AI context

### Combat foundation
- Fixed-position 1v1 baseline.
- 1 main Hero + up to 5 Pets/satellites.
- Pets act as turret/satellite units and have no HP in the current baseline.
- Hero has HP and Rage.
- Max Rage = 100.
- Hero baseline: HP 1000, ATK 100, DEF 20, Move Speed 5, Attack Interval 1.5s, Attack Range 1.8.
- Monster baseline: HP 500, ATK 50, DEF 10, Move Speed 3, Attack Interval 2.0s.
- Basic Attack Rage = 1.
- Rage On Damage = 1.
- Default Combo Rate = 1%.
- Default Counter Rate = 1%.
- Default Crit Rate = 1%.
- Baseline damage formula: ATK × multiplier × DefenseModifier.

### Skills
- 5 Hero skill types/slots: Normal Attack, Skill, External Skill, External Skill 2, Ultimate.
- Ultimate cannot be dodged and can crit.
- Skill behavior is data-driven.
- Multi-effect skill execution must consume Rage once and cooldown once.

### Banh Bao
- 1 Banh Bao = 1 skill usage in the normal monster screen.
- No Banh Bao means Hero cannot use skill even if cooldown is ready.
- Banh Bao does not affect Boss fights.

### Progression
- Hero Level is not direct base-stat scaling.
- Base Hero stats increase through Title Breakthrough / Đột phá Danh hiệu.
- D21 Level Cap is locked and must be preserved.

### Loot / D23
- 95% gear from chests; 5% from stage rewards/events under the current baseline.
- Normal monsters share the same Drop Rate.
- Each normal monster death drops 0 or 1 item.
- Chest Level = Drop Level.
- Chest Level determines item rarity/tier.
- Loot/rank/probability/chest progression is data-driven.

## D1-D20 status
The exact original text is not present in the current transferable context. Treat the original D1-D20 document as authoritative and do not invent replacements. When the user provides the original source, preserve exact terminology and semantics.

## D21 status
Confirmed as the Level Cap/progression baseline. Preserve existing implementation and design semantics.

## D22 status
The exact original D22 wording is not available in the current transferable context. Do not invent it. Preserve the original D22 source when supplied.

## D23 status
Confirmed as the Data-Driven Loot/Chest baseline described above. The original D23 document remains authoritative for any detail not reproduced here.

## Conflict policy
If code, an Antigravity proposal, or a future milestone conflicts with D1-D23, stop and report the conflict. Do not silently change the design contract.
