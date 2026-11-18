# Issue

**Title:** Tweak the way unindex task starts are logged

## Description

Only log after resolving indexer and indicate the name, thus clearing any eventual confusion of this line appearing multiple times in repeat.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9775fe3c7251`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.