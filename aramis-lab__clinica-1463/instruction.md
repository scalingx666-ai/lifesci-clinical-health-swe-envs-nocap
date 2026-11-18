# Issue

**Title:** [TEST][FIX] IXI-to-BIDS : Add non-regression tests for metadata files

## Description

Extends non regression tests to metadata files as part of #1450. The function writing sessions needed a little fixing.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f10bf6dc17c0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.