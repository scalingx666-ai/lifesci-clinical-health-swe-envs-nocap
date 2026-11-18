# Issue

**Title:** Change DICOM storage stop behavior to soft stop

## Description

#664 introduced a mechanism which stops the DICOM storage service's indexer worker thread when the service is stopped by request. An unwanted side-effect of this is that stopping the storage service will halt any pending requests to index files already in storage, leaving them in the state of stored but not indexed.

### Summary

- let the index queue worker thread finish processing all items in queue before exiting
- do not interrupt ongoing indexing tasks

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5fafbd325f37`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.