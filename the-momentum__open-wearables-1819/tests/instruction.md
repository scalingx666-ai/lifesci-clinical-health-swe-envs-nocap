# Issue

**Title:** refactor: add provider settings singleton, remove db/ raw repository calls from routes

## Description

add provider settings singleton, remove db/ raw repository calls from routes

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Refactor**
  * Standardized data retrieval for sign-in, developer listings, connection details, OAuth provider settings, scheduled synchronization, and invitation checks.
  * Sign-in responses, provider workflows, developer listings, synchronization behavior, and duplicate-email invitation responses remain unchanged.
* **Tests**
  * Added coverage for invitations using an email already assigned to a developer and for retrieving developers by email or listing all developers.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4e7108d1926d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.