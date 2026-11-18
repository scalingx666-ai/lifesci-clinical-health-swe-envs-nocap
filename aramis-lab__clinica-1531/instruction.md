# Issue

**Title:** [MAINT] Update poetry lock

## Description

Dependencies were not properly managed with poetry for release 0.10.0. This PR aims at fixing that by incorporating recent dependencies updates. Some tests for the anat-linear pipeline option `use-antspy` were also added. 

:warning: Pydra version was thresholded temporarily.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5dc7b3bf7eaf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.