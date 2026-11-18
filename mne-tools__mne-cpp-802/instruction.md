# Issue

**Title:** [MAINT] MNE Scan splash screen and logging debug

## Description

- Add mutex to logging function.
- Change splash screen hider to use signal/slots to call 'close()' instead of calling 'hide()' from separate qthread.

Ty @juangpc  for tracking down the logger issue and working through the splash screen issues

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7bc1e6a01507`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.