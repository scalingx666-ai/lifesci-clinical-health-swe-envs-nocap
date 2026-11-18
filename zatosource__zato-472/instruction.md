# Issue

**Title:** GH #471 Interval Based Scheduler not saving "repeats" argument

## Description

repeats argument is not stored when the service is invoked, it does work using the admin panel tho.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fba232b490cb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.