# Issue

**Title:** fix(server): quote header row cells

## Description

The `$csv` export now formats the header row the same way as the data rows. Every column name is quoted and escaped with the same helper used for data cells.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e9200d7f2045`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.