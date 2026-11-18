# Issue

**Title:** [FIX] OASIS3 converter adapted to current downloadable clinical data

## Description

In this PR I have modified the clinical data loading so that the user can directly point to the currently downloadable OASIS3_data_files directory. This directory contiains a wide variety of .csv files with all the necessary clinical and metadata information to reconstruct very similar tables to the previously used ADRC table.

In this manner, new users of the converter do not need to ask for the workaround to convert their OASIS3 datasets to BIDS. 

Additionally, adds a couple of loggers to print out progress in BIDS conversion, in a similar approach as in the ADNI converter.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f3e554274bf1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.