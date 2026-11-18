# Issue

**Title:** fix(manufacturing): count parallel operators once in the Job Card timer (backport #67474)

## Description

### Problem
The Job Card Elapsed Time timer added up every time log row. With two operators there is one row per operator for the same interval, so the timer showed twice the time, while Total Time in Mins (server) uses the union of the intervals.

### Fix
Compute the timer from the union of the time log intervals, as `get_workstation_minutes` does on the server.

### Steps to reproduce
1. Open the Job Card of a Work Order with one operation.
2. Click Start Job and select two employees.
3. After 60 minutes click Complete Job and reload the card.

Expected: the timer shows 01:00:00, like Total Time in Mins 60. Before: 02:00:00.

<hr>This is an automatic backport of pull request #67474 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f86f1fb9d983`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.