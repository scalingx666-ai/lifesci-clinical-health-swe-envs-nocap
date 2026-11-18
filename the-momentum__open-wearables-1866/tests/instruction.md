# Issue

**Title:** fix(backend): fall back to the same writer's heart rate for workout avg HR

## Description

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Average heart rate can now be calculated using samples from a workout’s original data source or, when those are unavailable, compatible sources from the same writer.
  * Workouts with no matching heart-rate samples are left without a calculated average.
* **Bug Fixes**
  * Average heart-rate results are processed in batches, including for large sets of workouts, while preserving each workout’s own result.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e5bd025bacc7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.