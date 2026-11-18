# Issue

**Title:** Segfault on gantry angle

## Description

Segfault when opening FIF files saved from MNE Python. Gantry angle is saved as FIFFT_FLOAT by MNE Python and as FIFFT_INT by mne-cpp.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9f46d3b4149b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.