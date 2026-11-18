# Issue

**Title:** [REF] Support SPM25 for `pet-volume`

## Description

This PR modifies the information and the documentation for the pipeline `PET-Volume` to recommend SPM25 standalone usage. Technically it also works with SPM12 as there were no change on SPM side.

What this PR does :
- Adapt the pipeline to SPM25
- Separates PET tests between surface and other pipelines
- Change the modules used for `pet-volume` to standalone

TODO : verify image integrity and thresholds for CI

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f3d1c175dbd6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.