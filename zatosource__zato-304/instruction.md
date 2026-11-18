# Issue

**Title:** Added migrations to RBAC related tables.

## Description

Removed also duplicated function _alter_column_nullable_false_ that had been already moved to util.py.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c70ba5d9ae34`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.