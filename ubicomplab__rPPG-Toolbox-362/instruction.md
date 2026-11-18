# Issue

**Title:** Add fixes for test-time chunk length

## Description

Akin to how `BigSmallTrainer.py` does it, these fixes make it so that, where relevant, the test-time chunk length config parameter is appropriately used. This likely didn't pop up as an issue since most folks would likely want to use the same chunk length as used during training, but I believe these fixes achieve the flexibility we were aiming for originally with the separate config parameters.

It should be noted that some trainer files are unaffected because they either use a frame num config parameter to control the temporal structure when instantiating a model (e.g., PhysNet and iBVPNet) or they operate on the entire input sequence (e.g., PhysMamba).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2152cf4368b4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.