# Issue

**Title:** Fixes an issue with fixed records, birthdates and timezones

## Description

When converting timestamps into LocalDates, the code was using the
local system timezone, when it should be using UTC. This was an issue
for some fixed records with a birthdate that happens in the year
before the start of Daylight Saving Time. This fix switches to using
UTC.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d4af94570aba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.