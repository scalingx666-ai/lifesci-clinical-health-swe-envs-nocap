# Issue

**Title:** Fix trigger subscription partition isolation

## Description

- Fixed `SubscriptionTriggeringSvcImpl#submitResource` to use `SystemRequestDetails.forRequestPartitionId` instead of `SystemRequestDetails.forAllPartitions()`
- IT test added
- change log

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2c21e2d2650f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.