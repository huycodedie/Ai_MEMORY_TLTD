Exit code: 0
Wall time: 0.6 seconds
Output:
# UI-02 â€” Combat Runtime Timing Verification Report

## Result

- **Runtime execution result:** **INCONCLUSIVE â€” not executed in this environment**.
- **Global UI-02:** **NOT LOCKED**.
- The monitor was changed to require real Play Mode evidence: Encounter 1 â†’ 2 â†’ 3, with completion counted only on `MonsterDeath`.

## Audit findings

### 1. Why movement appeared in 0.001â€“0.002 seconds

The previous monitor ran a tight synchronous editor loop and directly called:

- `hero.Movement.MoveTowardTarget(..., 0.05f)`;
- `currentMonster.Movement.MoveTowardTarget(..., 0.05f)`;
- `hero.Attack.ManualTick(0.05f)`;
- `currentMonster.Attack.ManualTick(0.05f)`.

Those calls advanced gameplay by synthetic `0.05s` steps while the wall-clock stopwatch advanced only a few milliseconds. The reported 0.001â€“0.002s values therefore measured editor-loop compression, not Unity frame runtime.

### 2. Manual simulation audit

The old monitor did manually advance movement and attacks and used a hard-coded `dt = 0.05f`. It did not call `Time.timeScale`, but the synthetic delta had the same invalid timing effect for this verification.

The replacement `Prototype01CombatRuntimeTimingMonitor` is an observer launched into Play Mode. It only samples `Time.frameCount`, `Time.time`, `Time.realtimeSinceStartup`, `Time.deltaTime`, `Time.unscaledDeltaTime`, transforms, movement and attack state from normal runtime components. It does not call `Tick`, `Update`, `Attack`, `ManualTick`, teleport, modify `Time.timeScale`, or increase MoveSpeed. The only test-only setup is additional Hero durability so three encounters can be observed.

### 3. AttackInterval source discrepancy

| Entity/value | Source | Finding |
|---|---|---|
| Hero 1.5s | `Assets/_Game/Data/HeroConfig.asset` â†’ `HeroConfigSO.attackInterval: 1.5`; `Hero.InitializeHero()` calls `Attack.Initialize(heroConfig.AttackInterval, ...)` | This is the runtime configured baseline in the current scene path. |
| Hero 1.0s | `HeroProgressionConfigSO.GetBaseStatsForLevel()` contains `StatType.AttackInterval = 1.0f` | This method is not used by `Hero.InitializeHero()` or `ApplyBaseStatsFromTitle()`; it explains the stale 1.0 claim, not the observed runtime component value. |
| Monster 2.0s | `Assets/_Game/Data/MonsterConfig.asset` â†’ `MonsterConfigSO.attackInterval: 2`; `Monster.InitializeMonster()` calls `Attack.Initialize(monsterConfig.AttackInterval, ...)` | This is the runtime configured baseline. |
| Monster 1.5s | Previous report hard-coded â€œMonsterConfig defaultâ€ as 1.50s | Stale report claim; current asset/code baseline is 2.0s. |

`StatusController.GetAttackIntervalModifier()` is sampled read-only. The effective interval is recorded as configured component interval plus that modifier; no modifier is injected by the monitor.

## Required telemetry per observed event

The updated monitor records for `MonsterSpawn`, `HeroMoveStart`, `HeroEnterAttackRange`, `HeroAttackDamage`, `MonsterAttackDamage`, and `MonsterDeath`:

`Time.frameCount`, `Time.time`, `Time.realtimeSinceStartup`, `Time.deltaTime`, `Time.unscaledDeltaTime`, Hero/Monster positions, effective MoveSpeed, configured/effective AttackInterval, attack timer/readiness, and config/modifier source.

## Execution limitation

Unity Editor executable was not available to this session. A `dotnet build Assembly-CSharp-Editor.csproj --no-restore` fallback could not run because the .NET Framework 4.7.1 reference assemblies/targeting pack are absent. Consequently no new Play Mode frame/death evidence is claimed here, and the report remains INCONCLUSIVE rather than PASS.

## Files changed

- `Assets/_Game/Editor/Prototype01CombatRuntimeTimingMonitor.cs` â€” instrumentation/test harness only.
- `PROJECT_MEMORY/UI-02_COMBAT_RUNTIME_TIMING_REPORT.md` â€” this audit and execution status.

