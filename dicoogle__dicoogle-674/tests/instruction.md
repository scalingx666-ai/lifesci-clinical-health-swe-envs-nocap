# Issue

**Title:** Webapp maintenance

## Description

Updates several dependencies and ensures the presence of the latest `dicoogle-client` 5.2.x in the webapp.

Requires Node.js >=16 to build the webapp (which everyone should have by now anyway).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `57ebdcfa261a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.