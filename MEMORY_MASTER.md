# TLTD AI MEMORY MASTER

## 1. Project identity
- Project: TLTD / Giang Ho Trong Tay
- Engine: Unity + C#
- Development environment: Windows, Google Antigravity IDE
- Local repository: `E:\code\TLTD`
- Architecture goal: modular, data-driven, extensible, testable, deterministic where required.

## 2. Mandatory response/audit behavior
- Respond in Vietnamese unless the user requests another language.
- Be direct, technical, structured, and evidence-driven.
- Preferred structure: conclusion -> passed -> failed/missing -> risks/audit -> next action -> prompt when needed.
- Never fabricate PASS, execution, visual verification, regression, or LOCKED status.
- Distinguish: IMPLEMENTED, EXECUTED, PASS, VISUAL VERIFIED, REGRESSION PASS, LOCKED.
- Automated test PASS is not the same as Unity Play Mode PASS.
- Play Mode PASS is not automatically visual verification.
- A report claiming PASS is evidence to audit, not a substitute for actual execution evidence.
- If a required test was not executed, say `NOT EXECUTED`.
- If implemented but not verified, say `IMPLEMENTED — NOT VERIFIED`.
- If visual evidence is missing, say `VISUAL NOT VERIFIED`.
- Only call a milestone LOCKED when all required evidence and regression conditions are actually satisfied.

## 3. Locked-design protection
- D1-D23 are the game's locked design contract.
- The original D1-D23 document supplied by the user is the highest-priority source of truth.
- Never silently change, reinterpret, simplify, or replace a locked D1-D23 rule.
- Never invent missing D1-D23 details.
- If a new implementation conflicts with a locked rule, STOP and report `ARCHITECTURE/DESIGN CONFLICT WITH LOCKED BASELINE`.
- Do not ask again about a decision already present in the locked baseline.
- If the original D1-D23 text is unavailable in a new chat, preserve this rule: do not reconstruct missing D1-D20 from guesswork. Obtain the original source once if a specific missing rule is required.

## 4. Architecture rules
- Audit repository before coding a new milestone.
- Find existing managers, authorities, components, ScriptableObjects, EventBus events, tests, and extension points first.
- Do not create duplicate runtime authorities.
- Prefer extending the existing system over creating a parallel system.
- Data that designers may tune should be data-driven/configurable rather than hard-coded when the architecture supports it.
- UI is presentation only and must not become the gameplay authority.
- Do not create a second damage pipeline, status pipeline, skill pipeline, or EventBus.

## 5. Core combat baseline
- Baseline combat is fixed-position 1v1 rather than free-roaming action combat.
- Player: 1 main Hero + up to 5 Pets/satellites.
- Pets act like turrets/satellites and have no HP under the current locked design.
- Hero has HP and Rage.
- Max Rage: 100.
- Hero baseline: HP 1000, ATK 100, DEF 20, Move Speed 5, Attack Interval 1.5s, Attack Range 1.8.
- Monster baseline: HP 500, ATK 50, DEF 10, Move Speed 3, Attack Interval 2.0s.
- Basic attack Rage gain: 1.
- Rage on damage: 1.
- Default Combo Rate: 1%.
- Default Counter Rate: 1%.
- Default Crit Rate: 1%.
- Baseline damage formula: ATK × multiplier × DefenseModifier.
- Do not invent or alter balance values unless explicitly approved.

## 6. Skills
- Hero skill structure has 5 skill types/slots: Normal Attack, Skill, External Skill, External Skill 2, Ultimate.
- Ultimate cannot be dodged and can crit.
- Skills are data-driven and use the existing execution/effect pipeline.
- Skill cooldown and priority rules must remain consistent with the locked design.
- Multi-effect skills must consume Rage once and apply cooldown once, not once per effect.

## 7. Banh Bao
- In the normal monster screen, 1 Banh Bao = 1 skill usage.
- If there is no Banh Bao, the Hero cannot use a skill even if its cooldown is ready.
- Banh Bao does not affect Boss fights.
- Offline/idle behavior must follow the locked design and must not be invented.

## 8. Progression
- Hero Level is used for progression/EXP and does not directly increase base Hero stats under the locked design.
- Base stats increase through `Đột phá Danh hiệu` / Title Breakthrough.
- D21 Level Cap is part of the locked progression baseline and must be preserved.

## 9. Loot / D23 baseline
- About 95% of gear comes from chests; 5% comes from stage rewards/events under the current locked baseline.
- Normal monsters share the same Drop Rate.
- Each normal monster death drops exactly 0 or 1 item.
- Chest Level is unified with Drop Level.
- Chest Level determines item rarity/tier.
- Loot rarity/tier/probability and chest progression are data-driven/configurable.
- Previously used example test state: 1,700,000 gold upgrade requirement and 974,470 current gold. Treat these as test/example values unless the original D23 source explicitly defines them as permanent balance.

## 10. Status architecture
- `EntityStatusController` is the authoritative runtime status authority.
- `EffectResolver` is the central effect resolution path.
- `SkillExecutor` is the skill execution path.
- `SkillExecutionValidator` validates skill use conditions.
- Do not create parallel DebuffManager/CCManager/CleanseManager/DispelManager/ShieldManager unless a repository audit proves the existing abstraction cannot support the feature and the user explicitly approves a redesign.

## 11. P07.5 locked
- Debuff / DoT / Status Tick.
- Reported automated: 46/46 PASS.
- Unity Play Mode: T01-T30 PASS.
- Master regression P01-P07.5: PASS.
- P07.5 is LOCKED.

## 12. P07.6 locked baseline
- Crowd control types: Stun, Root, Freeze.
- Effect Power Tier: A, B, C.
- `StatType.CcResistance`, clamped 0..1.
- Effective CC duration follows the existing resistance rule: base duration × (1 - resistance).
- 100% resistance blocks CC.
- Anti-CC immunity is checked before CC resistance.
- Freeze behaves like Stun for control purposes.
- Freeze Shatter occurs only when the applicable damage/effect has `CanShatterFreeze=true`.
- Root permits skills while restricting movement according to the established permission rules.
- Action permissions include `CanMove`, `CanBasicAttack`, `CanUseSkill`, `CanUseUltimate`, `CanDash`.
- Status flags include `IsStunned`, `IsRooted`, `IsFrozen`, `IsAntiCCImmune`.
- Movement and attack components enforce status permissions; skill validation enforces skill permission.
- Status modifiers integrate with Rage Gain, Healing Received, Damage Dealt, and Attack Interval.
- Do not duplicate this system.

## 13. P07.7 baseline
- Generic status removal lives in `EntityStatusController`.
- Cleanse removes negative statuses (Debuff, DoT, CC) according to target/category/selection rules.
- Dispel removes positive Buffs according to target/category/selection rules.
- Supports specific status, category, count, stacks, all negative/all positive as defined.
- Selection modes: Oldest, Newest, Random, HighestPriority, LowestPriority, All.
- Random test selection uses injected deterministic `RandomRangeProvider`; production randomness must not be weakened.
- Partial stack removal is supported; zero stacks are cleaned up.
- Preserve P07.5 stack/refresh/replace/max-stack semantics.
- Cleansing CC immediately restores permissions.
- Stun/Freeze interrupt behavior remains unchanged; Root does not gain an interrupt side effect.
- Cleansing Freeze must NOT trigger Freeze Shatter.
- Ordinary Cleanse/Dispel must NOT remove Anti-CC immunity unless an explicitly defined effect says so.
- CC Resistance remains unchanged by Cleanse/Dispel.
- EventBus includes status removal/cleanse/dispel/CC-cleanse events as implemented.
- Reported automated: 55/55 PASS; Play Mode: 35/35 PASS; Master Regression: PASS; 670+ total tests reported.
- Treat visual status as verified only if actual visual evidence exists; do not infer it from backend test counts.

## 14. P07.8 Shield / Barrier baseline
- Shield authority: `EntityStatusController`.
- Damage calculation authority: `DamageCalculator`.
- HP/damage application authority: `HealthComponent`.
- Shield interception is integrated into the existing `HealthComponent.TakeDamage` pipeline after damage calculation/modifiers and before HP decrement, as audited/reported for P07.8.
- Multiple shield ordering is deterministic: Priority descending -> StartTime ascending/FIFO -> ShieldId ordinal.
- No production random ordering.
- `ShieldTypes.cs`, `ShieldStackPolicy`, `ShieldAbsorbResult`, `RuntimeShieldInstance`, and `ShieldEffectDefinitionSO` are part of the reported P07.8 implementation.
- Reported stacking policies: Additive, RefreshDuration, Replace, Independent, Ignore.
- Zero shields must be cleaned up.
- No per-shield Update/coroutine/GameObject architecture.
- Shield must be safe for zero/negative damage, expired/removed shields, dead/destroyed targets, and multi-effect skills.
- Shield interacts through the existing damage/effect pipeline and must not create a second damage system.
- Shield is represented in status-removal categorization as `StatusRemovalCategory.Shield = 9`, but Cleanse/Dispel isolation must remain as defined.
- Shield events are integrated into EventBus.
- Reported automated: 55/55 PASS.
- Reported Play Mode: 35/35 PASS.
- Reported P05.1 regression: 40/40 PASS.
- Reported Master Regression P01-P07.8: PASS, 750+ tests, 100% PASS, zero regressions.

## 15. Current P07.8 blocker
A subsequent visual acceptance pass found:
- V01 Shield Application: FAIL.
- V02 Full Absorption: PASS.
- V03 Partial Absorption: PASS.
- V04 Shield Depletion: PASS.
- V05 Multiple Shields: PASS.
- V06 Real Combat: PASS.
- V07 Expiration/Removal: PASS.
- V08 BattleHUD: FAIL.
- Visual Verification: NOT VERIFIED.
- Code changes during that acceptance pass: NONE.
- Regression: PASS.
- P07.8: NOT LOCKED.
Reason: backend Shield behavior works, but BattleHUD/Prototype01 did not contain sufficient visible Shield UI representation for V01/V08 verification.

## 16. P07.8 remediation
- Do not rewrite P07.8 backend.
- Add only minimal presentation/debug/prototype Shield UI using the existing BattleHUD/HealthBarUI architecture where appropriate.
- UI must read authoritative Shield state from `EntityStatusController`.
- Do not duplicate Shield state inside UI.
- If multiple shields are displayed as an aggregate, it must be presentation-only and must not alter gameplay ordering or absorption semantics.
- Prefer existing EventBus shield events for UI refresh if compatible; avoid unnecessary per-frame polling.
- Shield UI should disappear/inactivate when Shield reaches zero.
- After remediation, run actual Unity Play Mode visual V01-V08, then rerun required automated tests and regressions.
- Only then can P07.8 be LOCKED.

## 17. Milestone history
- P06: Play Mode Acceptance 14/14 PASS; visual verification YES; LOCKED.
- P07.1: Automated 16/16; Play Mode 22/22; LOCKED.
- P07.2: Automated 22/22; Play Mode 39/39; LOCKED.
- P07.3: Automated 25/25; Play Mode 25/25; LOCKED.
- P07.4: Automated 45/45; Play Mode 36/36; Master 32/32 suites PASS; LOCKED.
- P07.5: Automated 46/46; Play Mode T01-T30 PASS; P06 14/14 PASS; Master P01-P07.5 100%; LOCKED.
- P07.6: Reported Automated 55/55; Play Mode 35/35; P06 14/14; P07.5 46 automated / 30 Play Mode; Master 100%; reported LOCKED.
- P07.7: Reported Automated 55/55; Play Mode 35/35; Master 100%; visual must not be assumed without evidence.
- P07.8: backend/test/regression PASS as above, but visual V01/V08 failed; NOT LOCKED.

## 18. Roadmap
P07.4 Heal + Buff -> P07.5 Debuff + DoT + Status Tick -> P07.6 Debuff + CC + Resistance + AntiCC -> P07.7 Cleanse + Dispel + Status Removal -> P07.8 Shield/Barrier -> P07.9 Advanced Skill Casting (Cast Time/Channel/Interrupt) -> P07.10 AOE/Multi Target -> P07.11 Projectile/Dash/Movement Skill -> P07.12 Advanced Combat Integration.
This roadmap is provisional beyond already-locked milestones; detailed future gameplay is not locked until explicitly approved.

## 19. P07.9 rule
Do not start P07.9 until P07.8 is actually LOCKED. Before implementation, audit SkillExecutor, SkillExecutionValidator, EffectResolver, SkillDefinitionSO, current CC interrupt behavior, Stun/Freeze/Root, EventBus, cooldown, Rage, and multi-effect execution. Extend existing systems; do not create a second interrupt system.

## 20. Final operating rule
If evidence and a report disagree, trust the concrete evidence. If design and implementation disagree, preserve the locked design and report the conflict. If something is unknown, say it is unknown rather than inventing it.
