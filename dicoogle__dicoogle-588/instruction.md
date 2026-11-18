# Issue

**Title:** Improve Java CI workflow

## Description

- update maven goals so that it checks the license and skips code formatting
- cache maven local repository

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f12ca02279e5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.