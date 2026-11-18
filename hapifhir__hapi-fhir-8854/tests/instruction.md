# Issue

**Title:** Support AND/OR combinations for date search params in JPA server

## Description

This fix replaces the use of DateRangeParam on the built-in JPA resource providers with DateAndListParam, which means combinations of AND and OR parameters are now supported.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dd4b5fc2457b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.