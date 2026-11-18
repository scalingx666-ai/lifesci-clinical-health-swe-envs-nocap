# Issue

**Title:** [sdk] Optimize Task memory usage after completion

## Description

### Summary

- when the task is done, remove references to callable and complete hooks so that the GC can sweep them
- add try-catch safeguard around completion hook calls
- reduce default capacity of `toRunWhenComplete` (usually only 1 or 2 hooks are attached, so there is no need for more capacity)
- override protected method `done()` instead of `set(V)` for calling complete hooks as well as the clean-up
- remove uses of raw types

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8a64b3770965`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.