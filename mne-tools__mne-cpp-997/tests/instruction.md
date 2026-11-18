# Issue

**Title:** mne_align: fix alias forward declarations for AcquiredPoints and PolhemusConnection

## Description

## Summary
Fixes C++ type conflicts in mne_align caused by forward-declaring alias types as classes.

## Changes
- Include acquired_points wrapper where AcquiredPoints is used and remove invalid class forward declarations.
- Include polhemus_connection wrapper where PolhemusConnection is used and remove invalid class forward declarations.

## Validation
- cmake --build build/developer-dynamic -j8 succeeds locally.
- Full ctest run was executed; multiple unrelated runtime failures remain in this environment.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5cf112121513`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.