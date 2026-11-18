# Issue

**Title:** [ENH][TEST] OASIS : move function `create_participants_df` from all converters utils to oasis utils

## Description

This PR aims at copying the `create_participants_df` function from all converters' `_utils` and the associated tests to OASIS and make the function more specific to this converter.


RQ : for this converter there is almost nothing to do. We could almost take the original excel and rename the columns. The reason we can't do that is that there is a duplicate column in the expected BIDS columns described in the specifications. To be more clear : in the original clinical data excel there is one column name `CDR` which is used to produced both `cdr` and `diagnosis_bl` column in the tsv output. Using a mapping to rename the column becomes complicated. I would be tempted to remove one line from the specifications and hard code the column to duplicate inside the function but it would be less explicit/explainable.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8da5c8208d07`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.