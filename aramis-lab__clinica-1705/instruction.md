# Issue

**Title:** [DOC] Update information for mrtrix3 and convert3d

## Description

## Description
The conda channels used for these tools do not support Mac (ARM) installation. Documentation was modified to indicate how to install clinica considering this. An additional yml for conda environment was added to handle this specific case.

## To Check :
- Command line : `conda env create -n test -f environment(...).yml`
  - [x] Works for Linux / Mac Intel (should not change existing behavior)
  - [x] Now works for Mac ARM
- Documentation builds properly

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ad9b048f661d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.