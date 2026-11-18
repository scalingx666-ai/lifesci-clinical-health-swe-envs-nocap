# Issue

**Title:** [ENH] MNE-Scan: show gof as well

## Description

<img width="322" src=https://user-images.githubusercontent.com/40984141/168338733-2916c8bc-fcae-4f71-b903-e045f7adaa06.png>

For a better understanding of whether fitting goes well and if the issue might be a particular coil, I added the Goodness of Fit (GoF ) next to the error in the `Quick Control` widget. 

In general, the error gives information about the transformation and the gof about the fit itself. So both should be presented next to each other

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `47e2de910986`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.