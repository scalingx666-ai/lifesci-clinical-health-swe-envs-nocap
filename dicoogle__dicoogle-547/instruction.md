# Issue

**Title:** Removed not used distribution management endpoints

## Description

Removed not used distribution management endpoints 
They were declared already in the parent `pom.xml` and create issues while deploying to remote maven repos.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `896d14e28392`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.