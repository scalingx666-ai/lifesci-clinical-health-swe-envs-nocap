# Issue

**Title:** Fix problems in unindexing servlet and documentation

## Description

### Summary

- Clarify and correct documentation around indexing/unindexing operations
   - While the force indexing endpoint does a recursive walk to index every file within the given base URI, the same is not the case for the unindexing operation
- Fix unindex servlet in series & study unindexing
   - it was still picking the wrong array of parameter values, so it would not work.
- Sanitize DICOM UID input in unindex servlet

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `96a0bba5d4de`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.