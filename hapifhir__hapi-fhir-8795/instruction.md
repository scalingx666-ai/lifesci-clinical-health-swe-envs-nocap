# Issue

**Title:** Fix auto-versioned references by ID to placeholder entries in transactions

## Description

## Description

In a transaction, an auto-versioned reference by ID (for example `Patient/123`) was saved without a version when the target's entry had a placeholder `fullUrl` (`urn:uuid:...`).

HAPI already versions references that use the placeholder `fullUrl`. However, HAPI did not map the resource ID to the new version, so references by ID were left unversioned.

Patient ID partition mode triggers this case, because Patient ID partition mode rewrites placeholder references to resource IDs before saving.

## Changes

- `BaseTransactionProcessor`: when an entry with a placeholder `fullUrl` is saved, also map the entry's resource ID to the new version.
- `RequestPartitionId`: added `isUnboundedAllPartitions()`. This method distinguishes "all partitions" without a list of partition ids.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3ef5fd1f0ebf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.