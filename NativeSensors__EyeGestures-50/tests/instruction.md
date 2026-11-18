# Issue

**Title:** making eyegestures recoverable if tracking is lost

## Description

Features:
- v3 is recoverable in case of error and returns Nones
- v2 is recoverable in case of error and returns Nones

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1fb6376eb2ab`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.