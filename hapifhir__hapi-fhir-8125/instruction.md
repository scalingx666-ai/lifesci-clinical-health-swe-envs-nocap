# Issue

**Title:** Patient ID partition mode: support conditional Patient references in transaction bodies and chained subject/patient searches

## Description

## Summary

In Patient ID partition mode, `PatientIdPartitionInterceptor` now handles two cases that previously failed — on storage that supports an all-partition (all-shard) search:

- **Patient inline match URLs in a transaction body** (e.g. `subject = "Patient?identifier=..."`): the new `STORAGE_TRANSACTION_WRITE_AFTER_PREFETCH` hook rewrites the reference to a literal `Patient/<id>`, reusing what the pre-fetch already resolved, so per-entry partition determination can route the resource instead of rejecting it with HAPI-1326.
- **Unresolved chained `subject`/`patient` search params** (e.g. `Observation?subject.identifier=...`): the search fans out across all partitions instead of failing with HAPI-2928.

Both are gated on `PartitionSettings.isAllPartitionSearchSupported()` (default `true`). On storage that cannot search across all partitions the previous single-partition behaviour is unchanged: such transactions are rejected up front with HAPI-1326 and such searches with HAPI-2928.

## Notes

- `isAllPartitionSearchSupported()` is a settable flag on `PartitionSettings` (default `true`); deployments whose storage cannot do an all-partition search opt out by setting it `false`.
- Only Patient-compartment references are rewritten; other references are left for the core transaction processor to resolve at save time.
- Transaction match-URL outcomes: one match → rewritten to `Patient/<id>`; no match → left untouched and rejected downstream with HAPI-1326; multiple matches → rejected by the pre-fetch with HAPI-2207.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a3bb2a9fbd65`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.