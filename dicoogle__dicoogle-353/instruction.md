# Issue

**Title:** Add error handling to query interface (Merge the #349)

## Description

It is the same PR made from @Enet4 - #349 

Quick modifications: merge with current dev branch and throw QueryException at QueryDimInterface.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `01813130734b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.