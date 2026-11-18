# Issue

**Title:** [FIX] Fix imports in  `pet-volume` after creation of pipelines.pet

## Description

Following PR #1497 there were some left-over imports that imported get_suvr_mask from `utils.pet`.

Adding the PR as these imports should be fixed while the pipeline is included in the new module (cf #1237).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4f907bc5f4f7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.