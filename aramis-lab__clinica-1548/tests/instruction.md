# Issue

**Title:** [ENH] `pet-volume` class `ApplySegmentationDeformation` should inherit from Nipype `ApplyDeformations`

## Description

This PR simplifies the class `ApplySegmentationDeformation` by basing it on Nipype `ApplyDeformations` which was the original inspiration.

RQ : to look at after other PET-volume PR

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f744eb00ef1f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.