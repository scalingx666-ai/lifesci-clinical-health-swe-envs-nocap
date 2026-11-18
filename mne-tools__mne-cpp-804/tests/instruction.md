# Issue

**Title:** [MAINT] Connect to ftbuffer on start

## Description

- Attempt to connect to FieldTrip buffer on pressing start in MNE Scan.

This is part of the functionality that was present in the 'ssadhd' branch, but just the ftbuffer stuff decoupled from the hpi debugging.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e94993ce4ac8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.