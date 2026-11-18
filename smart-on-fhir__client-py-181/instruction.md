# Issue

**Title:** oauth: handle a string expires_in value gracefully

## Description

If an OAuth token's expires_in field is a string instead of an int, simply try to convert it to an int first.

Fixes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `19f964c70d68`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.