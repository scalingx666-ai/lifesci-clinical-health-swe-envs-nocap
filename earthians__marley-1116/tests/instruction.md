# Issue

**Title:** fix: sales invoice - link patient to customer - error (backport #1115)

## Description

- if customer is left blank and link patient to customer is yes it throws error
- remove unused import<hr>This is an automatic backport of pull request #1115 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9f5d12689e5b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.