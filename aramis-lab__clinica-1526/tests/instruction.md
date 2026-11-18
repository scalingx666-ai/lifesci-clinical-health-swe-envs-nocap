# Issue

**Title:** [REF] UKB : Modify tsv writing to fit BIDS specifications

## Description

Following the work in #1450.

In order to facilitate new regression tests on metadata, this PR : 

- [x] Splits BIDS writing in participants/sessions/images/scans
- [x] Applies required modifications for scans to follow BIDS specifications
- [x] Tests scans writing (when logic is validated)
- [x] Should be accompanied by a PR data for CI (when logic is validated)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f1b47aa08286`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.