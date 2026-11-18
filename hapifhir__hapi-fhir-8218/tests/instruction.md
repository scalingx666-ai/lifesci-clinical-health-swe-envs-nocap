# Issue

**Title:** Jr 20260804 async mdm submit partition

## Description

Previously, the async version of the $mdm-submit operation was hardcoded to apply to all partitions. This PR adds code to derive the partition ID from the request details. This brings it into alignment with the sync version of the operation and with other async MDM operations such as $mdm-clear.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `52891f66f3a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.