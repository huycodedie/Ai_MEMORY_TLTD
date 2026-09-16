# TLTD AI MEMORY MASTER

## 1. Project identity
- Project: TLTD / Giang Ho Trong Tay / Thao Thiet Long Than Dao.
- Engine: Unity + C#; current project reports use Unity 6000.6.0f1 (64-bit).
- Development environment: Windows, Google Antigravity IDE.
- Local workspace: `E:\code\TLTD`.
- Long-term memory repository: `huycodedie/Ai_MEMORY_TLTD`.
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
- Later explicit user-approved amendments/revisions supersede older rules when the superseding relationship is proven.
- P01+ behavior that was actually tested and explicitly accepted/locked by the user can supersede older historical implementation descriptions.
- Never silently change, reinterpret, simplify, or replace a locked rule.
- Never invent missing D1-D23 details.
- If a new implementation conflicts with a locked rule and no superseding decision is proven, STOP and report `ARCHITECTURE/DESIGN CONFLICT WITH LOCKED BASELINE`.
- Do not ask again about a decision already present in the locked baseline.
- If the original D1-D23 text is unavailable in a new chat, preserve this rule: do not reconstruct missing D1-D20 from guesswork.

## 4. Architecture rules
- Audit repository before coding a new milestone.
- Find existing managers, authorities, components, ScriptableObjects, EventBus events, tests, and extension points first.
- Do not create duplicate runtime authorities.
- Prefer extending the existing system over creating a parallel system.
- Data that designers may tune should be data-driven/configurable rather than hard-coded when the architecture supports it.
- UI is presentation only and must not become the gameplay authority.
- Do not create a second damage pipeline, status pipeline, skill pipeline, EventBus, distance authority, or combat engine.

## 5. Core combat baseline
- Player: 1 main Hero + up to 5 Companions.
- Companion is a CombatEntity with HP, can be attacked, can die, and can respawn under the locked respawn rule. This is the current rule and supersedes older no-HP Pet/satellite wording.
- Hero has HP and Rage.
- Max Rage: 100.
- Hero baseline: HP 1000, ATK 100, DEF 20, Move Speed 5, Attack Interval 1.5s, Attack Range 1.8.
- Monster baseline: HP 500, ATK 50, DEF 10, Move Speed 3, Attack Interval 2.0s.
- Companion baseline attack interval: 2.0s.
- Basic attack Rage gain: 1.
- Rage on damage: 1.
- Default Combo Rate: 1%.
- Default Counter Rate: 1%.
- Default Crit Rate: 1%.
- Baseline damage formula: ATK × multiplier × DefenseModifier.
- Do not invent or alter balance values unless explicitly approved.

## 6. Skills
- Historical D6/D13 material describes Hero action/skill slots; exact historical counting wording must not override later P01+ tested implementation.
- Skills are data-driven and use the existing execution/effect pipeline.
- Skill cooldown and priority rules must remain consistent with the current locked design and tested P01+ behavior.
- Multi-effect skills must consume Rage once and apply cooldown once, not once per effect.
- Ultimate behavior, including its Rage requirement and targeting/dodge rules, must follow the current locked/tested implementation rather than an older prototype example when they differ.

## 7. Banh Bao
- In Normal Monster Battle, 1 Bun/Banh Bao = 1 Hero combat action, including Basic Attack, Skill actions and Ultimate.
- Companion actions do not consume Bun.
- When Bun reaches 0 during Normal Battle: Hero stops, Companions stop, and Normal combat stops.
- Boss fights do not depend on Bun.
- Offline/idle Bun behavior follows the locked D19 rules; do not invent additional behavior.

## 8. Progression
- Hero Level is used for progression/EXP and does not directly increase base Hero stats under the locked design.
- Base stats increase through `Đột phá Danh hiệu` / Title Breakthrough.
- D21 Level Cap is part of the locked progression baseline and must be preserved.
- If Hero reaches a Title Level Cap and cannot Breakthrough, additional EXP is retained/accumulated rather than lost; this supersedes an older historical reset-to-zero answer.

## 9. Loot / D23 baseline
- About 95% of gear comes from chests; 5% comes from stage rewards/events under the current locked baseline.
- Normal monsters share the same Drop Rate.
- Current locked baseline: each normal monster death drops exactly 1 item.
- `Chest Level = Drop Level = Cấp Rơi`; one concept and one runtime authority.
- Item Level is based on current Hero Level with `abs(ItemLevel - HeroLevel) <= 5`.
- Cấp Rơi determines rarity/quality availability and probability.
- The visible nine qualities in the reference UI are NOT the maximum rarity list. Higher qualities may exist.
- A quality at 0% may simply be unavailable/not unlocked at the current Cấp Rơi; it does not mean the quality does not exist.
- Rarity count, higher-rarity names, unlock thresholds, probabilities, and Item Level distribution inside ±5 remain data-driven/TBD unless explicitly locked.
- Equipment has 12 wearable slots: Vũ khí/Kiếm, Mũ, Khăn che mặt, Áo, Quần, Giày, Găng tay, Đai lưng, Áo choàng, Dây chuyền, Nhẫn, Bùa/Ngọc.
- Do not use `SPECIAL` as a player-facing slot name.
- Equipment recycle returns GOLD ONLY; no EXP.
- Base Auto-Recycle: item CP lower than equipped item is eligible; future Preferred Attribute/Affix protection may keep it.
- Previously used example test state: 1,700,000 gold upgrade requirement and 974,470 current gold. Treat these as test/example values unless a source explicitly defines them as permanent balance.

## 10. Status architecture
- `EntityStatusController` is the authoritative runtime status authority.
- `EffectResolver` is the central effect resolution path.
- `SkillExecutor` is the skill execution path.
- `SkillExecutionValidator` validates skill use conditions.
- Shield authority is integrated into `EntityStatusController` under P07.8.
- Do not create parallel DebuffManager/CCManager/CleanseManager/DispelManager/ShieldManager unless a repository audit proves the existing abstraction cannot support the feature and the user explicitly approves a redesign.

## 11. P07.5 locked
- Debuff / DoT / Status Tick.
- Reported automated: 46/46 PASS.
- Unity Play Mode: 30/30 PASS.
- Master regression through P07.5: PASS.
- P07.5 is LOCKED based on supplied execution evidence.

## 12. P07.6 locked baseline
- Crowd control types: Stun, Root, Freeze.
- Effect Power Tier: A, B, C.
- `StatType.CcResistance`, clamped 0..1.
- Effective CC duration follows: base duration × (1 - resistance).
- 100% resistance blocks CC.
- Anti-CC immunity is checked before CC resistance/application.
- Freeze behaves like Stun for control purposes.
- Freeze Shatter occurs only when the applicable effect has `CanShatterFreeze=true`.
- Action permissions include `CanMove`, `CanBasicAttack`, `CanUseSkill`, `CanUseUltimate`, `CanDash`.
- Status flags include `IsStunned`, `IsRooted`, `IsFrozen`, `IsAntiCCImmune`.
- Movement and attack components enforce status permissions; skill validation enforces skill permission.
- Status modifiers integrate with Rage Gain, Healing Received, Damage Dealt, and Attack Interval.
- Do not duplicate this system.

## 13. P07.7 baseline
- Generic status removal lives in `EntityStatusController`.
- Cleanse removes negative statuses according to target/category/selection rules.
- Dispel removes positive Buffs according to target/category/selection rules.
- Supports specific status, category, count, stacks and configured all-negative/all-positive operations.
- Selection modes include Oldest, Newest, Random, HighestPriority, LowestPriority and All where configured.
- Random test selection uses injected deterministic `RandomRangeProvider`; production randomness must not be weakened.
- Partial stack removal is supported; zero stacks are cleaned up.
- Preserve P07.5 stack/refresh/replace/max-stack semantics.
- Cleansing CC immediately restores permissions.
- Stun/Freeze interrupt behavior remains unchanged; Root does not gain an interrupt side effect.
- Cleansing Freeze must NOT trigger Freeze Shatter.
- Ordinary Cleanse/Dispel must NOT remove Anti-CC immunity unless explicitly defined to target it.
- CC Resistance remains unchanged by Cleanse/Dispel.
- Shield isolation remains intact.
- Reported automated: 55/55 PASS; Play Mode: 35/35 PASS; Master Regression: PASS; 670+ total tests reported.
- Visual status is not inferred from backend test counts.

## 14. P07.8 Shield / Barrier — LOCKED
- Shield authority: `EntityStatusController`.
- Damage calculation authority: `DamageCalculator`.
- HP/damage application authority: `HealthComponent`.
- Shield interception is integrated into the existing `HealthComponent.TakeDamage` pipeline after damage calculation/modifiers and before HP decrement.
- Multiple shield ordering: Priority descending -> StartTime ascending/FIFO -> ShieldId ordinal.
- No production random ordering.
- Stacking policies: Additive, RefreshDuration, Replace, Independent, Ignore.
- Zero shields are cleaned up.
- No per-shield Update/coroutine/GameObject architecture.
- Shield is integrated through the existing damage/effect pipeline and does not create a second damage system.
- `StatusRemovalCategory.Shield = 9`; ordinary Cleanse/Dispel isolation remains intact.
- Shield events are integrated into EventBus.
- Automated: 55/55 PASS.
- Play Mode: 35/35 PASS.
- UI Tests: 5/5 PASS.
- Visual Acceptance V01-V08: PASS.
- Required regression suites: PASS.
- Master Regression P01-P07.8: 100% PASS according to the latest user-provided report.
- P07.8 is LOCKED based on that acceptance evidence.

## 15. P07.9 — LOCKED
P07.9 = Advanced Skill Casting (Cast Time / Channel / Interrupt).
- Instant CastTime=0 executes synchronously.
- Cast progression and Channel progression are runtime-driven.
- Rage is consumed at Cast Start; interrupted casts receive no refund.
- Cast-time cooldown begins at Cast Complete; Channel cooldown begins when channel ends.
- Interrupted before completion has no normal cooldown.
- Casting locks movement.
- Stun and Freeze interrupt active Cast/Channel.
- Root does not interrupt.
- Ordinary damage does not interrupt.
- Existing `EntityStatusController` remains sole CC authority.
- Existing `Entity.InterruptCurrentAction` is the integration point.
- No second skill execution authority, global loop, coroutine/async timing authority, or Animator-dependent timing authority.
- Ultimate validation occurs before Rage deduction.
- Death/target-death invalid paths remain protected.
- UI is presentation only.
- Reported final evidence: Phase2.3 13/13 on three consecutive runs after test-only Dodge hardening; targeted regressions 234/234; full Master Regression 1043/1043; compile 0 errors/0 warnings.
- P07.9 was explicitly LOCKED by the user.

## 16. P07.9.1 — LOCKED
P07.9.1 = Hero Autonomous Skill Decision & Auto Combat.
- Auto ON: autonomous normal-skill decisions plus Basic Attack behavior.
- Normal skill priority: Priority DESC, SkillId ordinal ASC tie-break.
- Ultimate can preempt/interrupt Basic Attack windup according to tested current behavior.
- Auto OFF disables autonomous normal-skill/ultimate decisions while Basic Attack remains active according to tested behavior.
- Manual skills continue through the existing validator/executor pipeline.
- `HeroSkillDecisionController` only reads Rage; it does not own Rage mutation.
- Ultimate RageCost is read from `SkillDefinitionSO.RageCost`.
- Active Cast/Channel keeps `IsCasting` true and blocks Basic Attack.
- Existing P07.8/P07.9 authorities remain authoritative.
- Reported evidence: dedicated 16/16; P07.8 55/55; P07.9 Phase5.3 36/36; P07.9 Risk04 18/18; historical Master P01-P07.8 PASS; compile 0 errors/0 warnings; runtime scenarios A-E PASS.
- Full baseline: `PROJECT_MEMORY/P07_9_1_LOCKED.md`.
- P07.9.1 is LOCKED based on supplied execution evidence.

## 17. UI design baseline
- `PROJECT_MEMORY/UI_DESIGN_AUTHORITY.md` is the structural UI baseline.
- Game is 2D mobile portrait / vertical-first.
- Global bottom navigation is the game shell, not owned by Công Pháp.
- 5 primary navigation positions; center = Main Hub / Main Game Frame.
- Main Content Area changes for major systems; no second navigation framework.
- Công Pháp is a dedicated system screen/module.
- Exact labels/icons, artwork, spacing, font, colors and detailed interaction remain open unless separately approved.
- `PROJECT_MEMORY/UI_REDESIGN_SPECIFICATION.md` is an approved implementation specification, not a global gameplay lock.

## 18. UI-01 status
UI-01 Foundation was reported PASS:
- Portrait 1080x1920.
- `SafeAreaRoot -> MainGameShell -> MainContentArea + GlobalBottomNavigation` hierarchy.
- Safe Area uses `Screen.safeArea`.
- Debug controls moved to drawer.
- Compile 0 errors/warnings.
- P07.8 55/55, P07.9 Phase5.3 36/36, Risk04 18/18, targeted regression 109/109 reported PASS.
- Reported nav labels `Túi Đồ`, `Tâm Pháp`, `Đại Điện`, `Bang Hội`, `Thiết Lập` are implementation placeholders, not newly locked gameplay/design names.

## 19. UI-02 current status
- Global UI-02 is NOT LOCKED.
- Pre-implementation audit found TopHeader, MonsterUI, HeroUI, CastBarUI, Shield presentation, skill bar, Companion HUD, equipment/inventory overlay and DamagePopup still needing presentation work.
- UI must bind to existing authoritative runtime state and must not create duplicate gameplay authorities.

## 20. UI-02 Runtime Combat Height Fix — PASS / REMEDIATED
A runtime deadlock was confirmed after Monster #1 death:
- Encounter #1 Hero and Monster both used Y=-0.3 and combat worked.
- Encounter #2 legacy Monster spawn used Y=-1.2 while Hero remained at Y=-0.3.
- Movement used horizontal distance (`delta.y=0`) and stopped at AttackRange 1.8.
- Attack used full `Vector3.Distance`, making 3D distance exceed the 1.9 attack threshold when DeltaY was 0.9.
- Result: Movement stopped while Attack remained out of range, producing permanent deadlock.

Current remediation:
- `BattleManager.monsterSpawnPosition` changed from `(4,-1.2,0)` to `(4,-0.3,0)`.
- `Prototype01SceneBuilder` serializes the same spawn Y.
- `AttackComponent` now uses the same horizontal combat-plane distance model as Movement (`delta.y=0`, then magnitude).
- Spawned monsters reuse `UIProceduralTextureFactory.GetMonsterStandeeSprite()`, scale `(1.1,1.1,1)`, sorting order 10, `flipX=true`; legacy white placeholder and 3D `MONSTER` label removed.
- Reported dedicated validation: 12/12 PASS.
- Reported Play Mode scenarios A-L PASS across Encounters 1-3 without manual reposition.
- Reported regression: 125/125 across P07.8, P07.9 Phase5.3, P07.9 Risk04, P07.9.1.
- Reported compile: 0 errors / 0 warnings.
- Reported locked gameplay authorities untouched: SkillExecutor, SkillExecutionValidator, SkillCastState, CooldownManager, RageComponent, EntityStatusController, DamageCalculator, HealthComponent, BasicAttackProcessor, HeroSkillDecisionController.
- Status: `PASS / REMEDIATED` based on user-provided evidence. This does not globally lock UI-02.
- Do not revert this fix and do not replace it with a fake range-tolerance workaround.

## 21. UI-02 next immediate task
Create a test-only **Combat Runtime Timing Monitor** before further UI-02 presentation work.
Suggested files:
- `Assets/_Game/Editor/Prototype01CombatRuntimeTimingMonitor.cs`
- `PROJECT_MEMORY/UI-02_COMBAT_RUNTIME_TIMING_REPORT.md`

Monitor requirements:
- Measure real wall-clock and Unity runtime timing.
- Observe Encounter 1 -> 2 -> 3 (and 4 if possible).
- Record MonsterSpawn, HeroMoveStart, HeroEnterAttackRange, HeroFirstAttack, MonsterFirstAttack, FirstDamage, MonsterDeath, NextEncounterSpawn.
- Record available Hero/Monster positions, alive state, Rage, attack timer/interval, AttackRange, target state.
- Record DeltaX, DeltaY, horizontal distance, full 3D distance, attack threshold.
- Record `Time.realtimeSinceStartup`, `Time.time`, and `Time.timeScale`.
- Diagnostic deadlock timeout may be 5 realtime seconds; this is NOT a gameplay rule.
- Do not teleport entities, manually attack, manually correct Y, manipulate Time.timeScale, fake timing with Sleep/WaitForSeconds, or modify gameplay authority merely to expose timing.
- If an API is unavailable, report `[UNAVAILABLE_FROM_CURRENT_API]` rather than modifying production architecture.
- Timing test must not become a second combat/timer authority.

## 22. Critical verification lesson
Some earlier automated tests forced Hero and Monster to the same Y coordinate, which masked the actual Prototype01 spawn discrepancy. Future tests must include real scene runtime and multi-encounter transitions and must not repair the condition under test through fixtures, teleportation or manual actions.

## 23. Continuation / new-chat handoff
For a complete current-session package, read:
- `PROJECT_MEMORY/CHAT_HANDOFF_2026-09-16.md`

Continuation order:
1. Read `AI_RULES.md`.
2. Read `CURRENT_DESIGN_AUTHORITY.md`.
3. Read `D1_D23_LOCKED.md` and amendments.
4. Read `CHAT_HANDOFF_2026-09-16.md`.
5. If working on UI-02, read UI-02 audit/spec/report files.
6. Treat P07.8, P07.9, P07.9.1 as LOCKED.
7. Treat the Y-axis combat fix as the current runtime baseline.
8. Audit new PASS claims against concrete evidence.
9. Continue with Combat Runtime Timing Monitor, then UI-02 Combat HUD.
10. Do not globally lock UI-02 until required runtime/visual acceptance is complete.

## 24. Final operating rule
If evidence and a report disagree, trust concrete evidence. If design and implementation disagree, preserve the latest proven locked design and report the conflict. If a later explicit user decision supersedes an older rule, record it in `DESIGN_CHANGELOG.md`. If something is unknown, say it is unknown rather than inventing it.

## 25. Evidence qualifier
Execution counts, Play Mode results, visual results and compile results in this memory are user-provided project evidence unless explicitly independently executed in the current chat. Never convert a report claim into independent verification.
