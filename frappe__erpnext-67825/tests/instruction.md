# Issue

**Title:** fix(manufacturing): check Workstation Type job cards against the cards on its workstations (backport #67469)

## Description

### Problem
For a Job Card with a Workstation Type, the overlap and capacity check only looked at cards with the same Workstation Type. Cards made from a BOM operation with a workstation have no type, so a type-only card was scheduled and logged over them. When a free workstation of the type was found, the start moved back to the busy job's start, before the Work Order's planned start.

### Fix
- A card with a workstation is checked against all cards on that workstation.
- A type-only card is checked against the cards on the workstations of its type.
- When a workstation of the type is free for the whole window, take it and keep the requested start.

### Steps to reproduce
1. Keep capacity planning on. Create Workstation Type T and workstations WS1 and WS2 of type T (capacity 1, no working hours).
2. Submit a Work Order for 10, planned start 08:00, whose BOM operation has Workstation WS1 (12 minutes per unit). Its Job Card is scheduled 08:00-10:00 on WS1.
3. Submit a Work Order for 10, planned start 09:00, whose BOM operation has only Workstation Type T (6 minutes per unit).

Expected: its Job Card is on WS2, 09:00-10:00. Before: on WS1, 09:00-10:00, over the first card.

<hr>This is an automatic backport of pull request #67469 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f86f1fb9d983`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.