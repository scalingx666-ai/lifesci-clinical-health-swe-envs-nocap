# Issue

**Title:** Rollback of:

## Description

Rollback of:
Start validating Reference Ids inside Element References.

- Modifies affected tests to replace invalid `reference_id`s with valid ones.
- Removes some unused imports.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6e04c5ec9f8c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.