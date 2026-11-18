# Issue

**Title:** BFD RIF Minimal Set

## Description

This PR adds functionality to create a minimal set of RIF files with coverage for all claim types.

- Export summary CSV with counts of claims per beneficiary by claim type
- Add new Gradle task to filter exported RIF files to create a new set that includes only enough beneficiaries to cover all claim types

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `842ca4be64c4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.