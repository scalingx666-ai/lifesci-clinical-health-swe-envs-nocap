# Issue

**Title:** Update repo setup to use pip for PyTorch installation and include uv

## Description

This PR does the following:

- Removes usage of the conda channels for PyTorch-related installations. This is in light of the following announcement that suggests, without the change in this PR, issues may occur in the future: 
- Adds [`uv`](https://docs.astral.sh/uv/) as an option to manage an environment for the toolbox.

I've tested both `conda` and `uv` environments using this PR and various parts of the toolbox (e.g., training, inference, and visualization of preprocessed data) without any issues. I expect the `conda` usage, which will continue to be used by almost all users in the near-term, to be unaffected, but the `uv` usage by anyone who wants to adopts it may be a bit bumpy given `uv` being relatively new.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `57e4de485bc7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.