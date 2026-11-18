# Issue

**Title:** Make the DICOM Storage SCP indexing queue to be asynchronous and independent task manager for queries (v3)

## Description

This PR introduces two changes:

- Make the DICOM Storage SCP indexing queue to be asynchronous 
- independent task manager for queries (v3)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0873180c1575`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.