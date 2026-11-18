# Issue

**Title:** Make Find SCP resilient to missing query-retrievel level

## Description

Fixes a server error situation when the FIND SCP service receives a malformed request with a missing Query/Retrieve Level.

### Sumary

- if query-retrieve level is missing or could not be matched, send error response
- use getString to retrieve DICOM text value
- clean up code a bit, removing commented out code and unwanted prints

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `74e3b9fca646`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.