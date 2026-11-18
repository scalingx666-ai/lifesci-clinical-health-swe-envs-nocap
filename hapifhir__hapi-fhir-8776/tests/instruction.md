# Issue

**Title:** Fix transaction retries failing with a false duplicate unique index error

## Description

Previously, when a FHIR transaction containing a resource with a unique combo search parameter was retried after a version conflict, each retry failed with HAPI-2883 and incorrectly reported a duplicate unique index within the transaction. The unique indexes recorded by a failed attempt are now cleared before retrying.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `90acf5be2d53`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.