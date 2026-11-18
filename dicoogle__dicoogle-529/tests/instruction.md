# Issue

**Title:** Add missing plugin info properties in /plugins

## Description

- query/index dim & storage default from server settings
- remove "endpoints" from servlet plugins, we don't have that information yet

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5507ee7d8b8b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.