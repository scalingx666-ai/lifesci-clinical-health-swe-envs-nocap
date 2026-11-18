# Issue

**Title:** fix: Catch SDK sleep lock failure

## Description

## Final scope

> _Added during review by Sebastian Kalisz._

The sleep lock is per user, so it is busy when another batch of the same user is saving sleep (a historical export sends many at once), or `finalize_stale_sleeps` is closing their night; a Redis outage raises a `ConnectionError` instead. A retry therefore does help, and nothing has to be lost:

- `handle_sleep_data` raises `LockError` on a busy lock instead of skipping the sleep silently (kept from this PR).
- New `save_sleep` (used by the SDK import and both Apple XML imports): the rest of the batch is saved now; the sleep goes to a new Celery task, `save_sdk_sleep` (SDK queue), which retries it for about 7 minutes (30 s, growing). Only when the lock stays busy through every attempt is the loss logged as an error and reported to Sentry.
- Before, a busy lock in the XML imports would now have aborted the whole file import; they defer the sleep the same way.

The `partial` run status from this PR is dropped: with the sleep retried there is no drop to report, and `partial` for every batch with a record rejected by validation would change `sync.completed` for all clients (it also could not stay `partial` in the Redis run summary or in the historical export's single `sync.completed`). The sync status contract stays as on `main`.

## Breaking change

> _Added during review by Sebastian Kalisz._

None.

The original description is kept below, struck through.

~~When the per-user sleep lock can't be acquired, the SDK sleep handler used to drop the batch's sleep without telling anyone: the run ended `success` and the client never knew to resend. Now only that sleep is lost, the run ends `partial`, and the failure shows up in logs~~

~~This should be a very rare case, where a lock is not acquired within a blocking timeout of 15s which would proabably signify issues with Redis <-> worker connection, but it was still uncaught regardless, so a retry wouldn't help here IMO (as stated in issue comment). Though afterwards, i did see someone implementing this on their fork: , also describing their issue~~

~~- Raising `LockError` instead of logging a warning and quietly returning.~~
~~- catching the error around sleep handling, the records are added as dropped.~~
~~- a batch with drops now marked as `PARTIAL` instead of `SUCCESS`.~~

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Sleep data is now retried when it can’t be saved because another process is using it, rather than being silently skipped.
  * Sleep records are counted and included in the reported sleep span only after they’re successfully saved.
  * Sleep data from SDK and file imports can be processed separately from other records when a save is delayed.
  * After repeated unsuccessful attempts, the sleep save is reported as dropped.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `27549f81ed48`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.