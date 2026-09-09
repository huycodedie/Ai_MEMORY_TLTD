# Ai_MEMORY_TLTD

Persistent AI memory / project decision repository for the TLTD Unity game project.

## Purpose

This repository is the persistent source of project decisions, locked design contracts, architecture constraints, milestone status, validation rules, and handoff context used by AI assistants working on TLTD.

## Source-of-truth hierarchy

1. Original D1-D23 design document supplied by the user — highest priority.
2. Explicitly LOCKED project architecture and milestone decisions.
3. Verified repository/runtime evidence and test logs.
4. New proposals — proposals are NOT locked until explicitly approved.
5. General AI/game-development knowledge — must never override the above.

## Critical rule

If a new implementation conflicts with a locked decision, STOP and report the conflict. Do not silently redesign, reinterpret, or invent missing rules.

## Current state

- Project: TLTD / Giang Ho Trong Tay
- Unity + C#
- Repository: E:\\code\\TLTD
- IDE: Google Antigravity
- Current milestone: P07.8 Shield/Barrier visual verification remediation
- P07.8 backend/runtime: reported PASS
- P07.8 visual verification: NOT VERIFIED / NOT LOCKED because V01 and V08 failed due to insufficient Shield UI visualization
- Do not start P07.9 until P07.8 is actually LOCKED.

See `MEMORY_MASTER.md` for the consolidated handoff and `D1_D23_LOCKED.md` for the D1-D23 contract status.