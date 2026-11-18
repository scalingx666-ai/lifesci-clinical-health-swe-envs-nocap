# Issue

**Title:** Data validation changes

## Description

This PR makes two key changes:

1. Each trainer is modified such that code related to the validation dataset and model selection is NOT executed when USE_LAST_EPOCH is set to True.
2. Main.py and config.py are modified to better indicate to users whether or not the validation dataset matters and to catch any weird behavior a user may encounter if they modify their configuration file incorrectly.

I don't think the config (YAML) files themselves have to be updated, especially since any additional functionality related to using a validation dataset (e.g., preprocessing, loading) should only ever occur if a validation dataset is actually being used for model selection in subsequent testing.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `970fe8c247a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.