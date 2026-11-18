# Issue

**Title:** Add experimental partial index on Task

## Description

Task is a workflow oriented resource type where the majority of resources settle on the terminal `Task.status` of `completed`. Most searches filter for various non-`completed` status, but the skew of that data often results in many rows being removed by filter putting significant CPU load on the DB.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `81d38472958a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.