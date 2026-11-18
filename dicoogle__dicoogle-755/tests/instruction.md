# Issue

**Title:** Merge maven frontend plugins into one

## Description

Trying to fix the error reported in the [previous check](https://github.com/dicoogle/dicoogle/actions/runs/40717376575/job/122918630078?pr=754) done via #754.

### Summary

- update frontend-maven-plugin to 1.15.4
- update downloaded versions of node and npm to the latest LTS
- combine executions together into the same plugin declaration

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1071b98f558e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.