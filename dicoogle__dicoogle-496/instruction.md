# Issue

**Title:** Make the DICOM Storage SCP indexing queue to be asynchronous

## Description

Make the DICOM Storage SCP indexing queue to be asynchronous.
As a consequence, a new task manager instance was created for query to avoid overload of index tasks, and avoid starvation of query tasks.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b4be3f1bc336`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.