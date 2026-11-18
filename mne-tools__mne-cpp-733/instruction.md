# Issue

**Title:** [FIX] Fix speed of model rotation

## Description

This PR includes:

- Docu fixes in Renderable3DEntity
- Fix applying the same rotation animation on the parent and children of a Renderable3DEntity. This led to <the number of children> faster animations. We now only apply the animation on the parent. This solves one problem reported in #731.
- Make use of parallel animation starting via `QParallelAnimationGroup`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cacf58ec319c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.