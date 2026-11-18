# Issue

**Title:** feat(polhemus): add resetRegistration() to PolhemusCoregistration

## Description

Clears headToWorld, headToDevice and sets registrationValid=false, then emits registrationChanged. Called when the user clears all acquired points so no stale transform remains active.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5cf112121513`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.