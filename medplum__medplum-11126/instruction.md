# Issue

**Title:** chore(server): log SMART scopes with partial permissions

## Description

When issuing tokens, log the SMART scopes whose combined permissions for a resource type are neither read-only (rs) nor full access (cruds), with the client and project.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6141a52812f6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.