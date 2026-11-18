# Issue

**Title:** Upgrade Spring Framework from 7.0.8 to 7.0.10

## Description

Resolves 17 Spring Framework CVEs fixed in 7.0.9 (6 Critical, 6 High, 4 Medium, 1 Low). 7.0.10 also fixes regressions introduced in 7.0.9.

Closes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `96ed05a3c94d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.