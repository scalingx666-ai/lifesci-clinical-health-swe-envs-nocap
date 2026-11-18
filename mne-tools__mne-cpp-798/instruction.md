# Issue

**Title:** [MAINT] BabyMEG plugin tweaks

## Description

- Remove blocking check for initialization of FiffInfo before it can be initialized.
- Remove 'Connect' tab and associated functions.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2cb1cf3ebaf3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.