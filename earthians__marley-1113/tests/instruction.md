# Issue

**Title:** fix: failing tests (backport #946)

## Description

- pass currency to get item details
- inpatient record: default currency if no currency is supplied while admitting patient
- add type hints to whitelisted functions<hr>This is an automatic backport of pull request #946 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `759166ba3b8d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.