# Issue

**Title:** fix(server): reject rescope to server when the email is already in use

## Description

Server-scoped Users are found by email alone, so rescoping a project User to server scope now fails if a server-scoped User with the same email already exists. The transaction is serializable to avoid a race with a concurrent create.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fce7a9045ce7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.