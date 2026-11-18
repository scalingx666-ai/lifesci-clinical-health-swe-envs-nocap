# Issue

**Title:** Add warning when transfer dataset has fewer batch effect levels than training data

## Description

While exploring the transfer functionality in PCNtoolkit, I noticed that it is possible to run a transfer when the new dataset contains fewer batch effects than the dataset used to train the original model. In such situations, the transfer step may still run, but the correction could potentially be biased because the model was trained with a larger set of batch effect levels.

To make this situation clearer to users, this change adds a warning when the transfer dataset contains fewer batch effects than the training dataset. The goal is simply to make users aware of the potential issue so they can interpret the results more carefully.

This change does not modify the underlying behavior of the model; it only adds a warning to improve transparency during transfer operations.

Happy to adjust this if a different warning message or placement would be preferred.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `04ea676d3178`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.