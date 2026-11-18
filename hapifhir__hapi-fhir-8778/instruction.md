# Issue

**Title:** Allow subclasses to override how ResourceVersionSvcDaoImpl reads versions

## Description

Moves the database version lookup in `ResourceVersionSvcDaoImpl` into a new protected method, `populateVersionsUsingDatabase`, so that a subclass can change how versions are read.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `895e2598e00d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.