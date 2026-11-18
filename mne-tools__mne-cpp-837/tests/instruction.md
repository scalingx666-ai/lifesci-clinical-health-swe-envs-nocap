# Issue

**Title:** [Fix, Enh]: Implement new coil ordering function

## Description

This PR solves the long ongoing struggle with unsuccessfully fits in some occasions. I figured that the issue was related to incorrect coil ordering. After a lot of debugging, it turned out that the current function `findOrder(...)` has its limitations. The issue with the current method is that it depends on the goodness of the fit. However, if a coil fit is bad due to bad placement etc. the algorithm can't really assign it to a position. Therefore I implemented an easy 'closest distance' algorithm. It assigns the fitted point to the closest digitizer. This approach is much faster than before and it facilitates the dipole fitting results in good locations despite the bad fitting quality.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6a2afd92c32b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.