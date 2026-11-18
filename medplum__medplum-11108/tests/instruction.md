# Issue

**Title:** fix(ci): fall back to empty service credentials instead of null

## Description

A null credentials expression is coerced to an empty string and still fails template validation on fork PRs. An empty mapping passes and makes the runner pull without logging in.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1f99ee4ff744`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.