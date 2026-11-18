# Issue

**Title:** [REF] T1/FLAIR-Linear : set higher value for N4BiasFieldCorrection b-spline parameter

## Description

As pointed out, b-spline parameters were different for FLAIR and T1 Linear. As is, the N4BiasFieldCorrection model from ANTs uses 4 fitting steps, dividing the b-spline parameter by 2 each time. If the input parameter is 600 mm, the last resolution of the b-spline grid would be 75 mm. If the b-spline parameter is lower, then structural differences can be mistaken for bias field (which was happening with 100mm for FLAIR). For balance between correction and safety, we put the parameter to 200 mm.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e633afc89e67`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.