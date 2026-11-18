# Issue

**Title:** [TEST][REF] Refactor and test functions related to creating participants.tsv for AIBL

## Description

Close #1351, close #1354

For other PR :  add non-regression tests that compare inside tsv for participants, scans and sessions

Remark : with this PR the patients that are in the BIDS but not in the clinical data are just filled with nans, they are not ignored

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `424b25defbef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.