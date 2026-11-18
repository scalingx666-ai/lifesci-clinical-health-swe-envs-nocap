# Issue

**Title:** [sdk] Undeprecate StorageInterface#handles

## Description

. Starting from either version 3.4.0 or 4.0.0, we will allow plugin developers to adjust how the URI is checked to know whether it can be handled by their plugins.

I am sending in the corresponding change in the learning pack soon.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `71e1d82c82d7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.