# Issue

**Title:** Improve indexer queue worker thread handling

## Description

This PR resolves some known issues with the DICOM storage indexer worker thread, most importantly:

- The indexer thread is taken down when DICOM storage is stopped ().
- If the indexer thread dies, the incident is logged and the DICOM storage service is stopped to prevent further damage. We do expect IT to intervene at this stage. An alternative would be terminating the whole archive.

### Summary

- The indexer thread was given the name `indexer-queue-worker`
- Define indexer thread with a `Runnable` instead of a `Thread` subclass
- Add logic to take down the old indexer worker thread when DICOM storage is stopped.
   - if DICOM storage service is stopped, flip `workerShouldExit` flag and interrupt thread
- Add exception handler to indexer queue worker for damage control. DICOM storage service is disabled automatically, which prevents the archive from accepting files that will never be indexed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c594989fae82`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.