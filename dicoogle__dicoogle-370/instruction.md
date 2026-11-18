# Issue

**Title:** Extend StorageInterface with `list`

## Description

Here's my quick proposal to address #261. It enables storage plugins to easily and efficiently provide directory listing. Please see the documentation for details. Support for listing is optional, but should be fairly easy to implement, so it won't make plugins harder to migrate.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8748eac7e071`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.