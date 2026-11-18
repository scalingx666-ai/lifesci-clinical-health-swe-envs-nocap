# Issue

**Title:** imp/Remove uri from default search servlet fields

## Description

This PR removes `uri` from the default search result fields, in order to prevent replicating this information inadvertently.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ecafbad96bb9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.