# Issue

**Title:** Drop MySQL support and remove the MySQL JDBC driver

## Description

- Remove MySQL from docs
- Indicate removal of support 
- Drop jars from the classpath

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b5b0ae759782`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.