# Issue

**Title:** DicomStorage: Add guards on unexpected exceptions

## Description

Increase robustness and introspection of the DICOM storage service.

- create slf4j logger in `DicomStorage`
- wrap DICOM storage executor around logging executor
- add debug log line at `cstore`
- extend catch to Exception at `onCStoreRQ`
- extend catch to Exception at `Indexer.run`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7325c9fa20fd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.