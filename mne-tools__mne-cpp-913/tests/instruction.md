# Issue

**Title:** Correct windows output paths and add add parallelization

## Description

Correct extraneous build-type folders in windows builds but setting build specific output dirs.
Add windows specific parallelization flag.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `34d488c3e449`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.