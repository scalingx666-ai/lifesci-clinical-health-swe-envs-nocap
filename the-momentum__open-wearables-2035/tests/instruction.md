# Issue

**Title:** fix: Lock only `event_record` on adjacent sleep lookup

## Description

Around midnight UTC today, our Sentry reported an issue regarding a deadlock during SDK sleep finalization. Each one of the deadlocks killed the `process_sdk_upload` task and rolled back the sleep part of the batch.

The pg log showed two things:
- Dirty day rollup (`SeriesRollupRepository.roll_up`) inserts `series_aggregate` with a FK on `data_source`, then `roll_up_sessions` upserts `event_record_aggregate` with a FK on sleep record
- sleep finalization (`find_adjacent_sleep_record`) with a `SELECT` query locks sleep record, and then data source

This caused an issue where two transactions take locks on data source and event record in opposite orders, which causes a deadlock (with a 1s default deadlock timeout)

I managed to reproduce it locally, and the fix is as follows:

During sleep finalization, in the SELECT query only `event_record` is locked (`of=self.model`) instead of locking matching rows in every joined table, since sleep finalization will never modify `data_source`, so it is safe; only `event_record` is gonna be merged together. Now `event_record` is the only row that both of these transactions want, so one will simply wait for the other.

_(Added during review by Sebastian Kalisz:)_ A test pins the lookup's lock to `FOR UPDATE OF event_record`, so a later change of the query cannot bring the `data_source` lock, and the deadlock, back. No breaking change.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Limited locking during adjacent sleep record lookups to the event record, preventing unrelated rows from being locked.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `30470f4f4a53`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.