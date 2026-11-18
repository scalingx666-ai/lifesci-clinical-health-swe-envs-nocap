# Issue

**Title:** [FIX] GENFI : sort dicoms before dropping duplicates

## Description

Dicom dataframe was filtered, starting by dropping duplicates on one column. If the dataframe was not previously ordered on an adjacent column there was a possibility to not get the same output each time. This caused failing non-regression tests when comparing scans.tsv files. 

Current non-regression tests for GENFI can be expected to fail with this PR but should not when #1468 is rebased

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `173b6444acc4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.