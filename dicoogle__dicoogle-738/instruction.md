# Issue

**Title:** Update dicoogle-client to v6

## Description

This allows us to check whether we are ready to start using `dicoogle-client` v6 everywhere.

### Summary

- dicoogle-client 6.0.0
- update servicesStore to use promise-based operations
- update exportStore
- Update Web UI module servlet to support ES module dicoogle-client

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f0ede27cd3e5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.