# Issue

**Title:** Fix a bug while deleting a study with too many images

## Description

This change increases the default maxFormContentSize to allow operations such as unindex/delete over large studies (with >3k image).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0f8d96ae98e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.