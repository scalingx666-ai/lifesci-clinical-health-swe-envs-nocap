# Issue

**Title:** feat(backend): run expensive data migrations once per instance

## Description

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Operational Improvements**
  * Expensive data migration scripts now record successful runs, skip work that has already completed, and retry after failures or interruptions. Concurrent startup runs are coordinated so only one instance performs a migration.
  * Dry runs do not mark migrations as complete; completed migrations can be run again when needed.
* **Documentation**
  * Added guidance on when and how to use run-once data migration scripts.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f9d9a88ddd1d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.