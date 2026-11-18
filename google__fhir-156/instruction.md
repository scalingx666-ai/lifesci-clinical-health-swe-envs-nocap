# Issue

**Title:** Bumps com.google.http-client and guava maven versions to latest.

## Description

Bumps com.google.http-client and guava maven versions to latest.

Fixes test that breaks due to change in how http-client serializes schema as strings.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `822e2ba5c712`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.