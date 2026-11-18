# Issue

**Title:** Remove dangling /management/plugins/ endpoint

## Description

.

### Summary

- convert int constants for service type to an enum
- remove servlet handler for "/management/plugins/"
- document servlet operation methods

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `15c65f503932`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.