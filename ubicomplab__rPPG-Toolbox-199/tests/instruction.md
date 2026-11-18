# Issue

**Title:** Output vizualization

## Description

Ability to dump model outputs and labels (from neural method testing) to a .pickle file - added to all model trainers (other than BigSmall). Added an associated python notebook to visualize labels and predictions from the output .pickle file. Also added associated readme information.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b5e203b84663`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.