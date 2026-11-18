# Issue

**Title:** [MAINT] MNE Analyze - filter control update

## Description

FilterDesignView/FilterViewSettings:
- Make simple filter control show changes made in filter designer (and vice versa)
- Make simple filter control show defaults from filter designer when initiated.
- Load available filter design methods from FilterKernel

FilterKernel:
- Add new FilterParameter class to replace enums.
- Add static vectors in for design method and filter types to replace enums and static conversion functions.

ScalingView/FiffRawViewSettings:
- Change default loaded values


 

ty Juan

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8f92259ca015`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.