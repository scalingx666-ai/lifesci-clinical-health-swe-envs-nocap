# Issue

**Title:** MMPD Fixes

## Description

Fix Mini-MMPD motion label error, add label error handling, and fix YAMLs

I generally added label error handling to the `MMPDLoader.py` file. Also fixed the associated YAML configs that use pre-trained models for testing - previously, the YAML config files used a pre-trained model file-path that would not work out-of-the-box for other toolbox users (including myself).

@McJackTang, my suspicion when you tested your previous PR (#134) is that you either used a different version of the MMPD dataset that you have locally and happens to have different motion labels, or perhaps there is some mistake in the labels in the MMPD dataset that was released and shared with dataset users via OneDrive and Baidu NetDisk. Either way, the error I ran into had to do with the motion labels for stationary motion not just being read as `Stationary` and `Stationary (after exercise)` as per the existing code in `MMPDLoader.py`, but also `Watching Videos`. My assumption is that `Watching Videos` also corresponds to a motion level of 1, or stationary motion type. Without the inclusion of `Watching Videos` as a potential label corresponding to the stationary motion type in this PR, users will encounter the same error I did and will be unable to use the dataset after pre-processing. The error ends up being encountered with this line when a motion label is not properly recognized and therefore an integer value is not present:

https://github.com/ubicomplab/rPPG-Toolbox/blob/b483b40217edaefc00de595dea83a99b58517681/dataset/data_loader/MMPDLoader.py#L162

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b483b40217ed`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.