# Issue

**Title:** Update pyproject

## Description

A quick path to add pytorch and numba to the dependencies. This fixes the two-step install and should make uploading to Pypi easy. 

A downside to this is that users of an HPC cluster with non-cuda login nodes and cuda compute nodes may need to manually replace their pytorch installation with the correct one if they installed the toolkit from a login node and want to run it from a compute node. However, since this patch makes life easier for all users, and the downsides only affect a small number of users (users of the NP or RFA models), and for those, the fix is quite straightforward, I believe the benefits outweigh the downsides.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `80d82d23f9bc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.