# Issue

**Title:** [TEST][FIX] GENFI-to-BIDS : Add comparison of metadata files in non-regression tests

## Description

Extended non-regression tests for metadata files as part of #1450.

Fixes : 
- To follow BIDS specs : name of metadata files to "scans" instead of "scan" ; name of field "filename" instead of "bids_filename" in the scans metadata file
- Modification of dataframe operations for participants metadata file because there were duplicate lines

See data PR:

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9844626439f2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.