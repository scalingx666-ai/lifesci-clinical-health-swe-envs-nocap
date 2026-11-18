# Issue

**Title:** refactor(backend): fetch event records and data sources via repositories in detail webhooks

## Description

## What does this change?

`EventRecordService` no longer queries `EventRecord` and `DataSource` directly when emitting detail webhooks. It goes through the repositories, using a new generic `CrudRepository.get_by_ids` built on the 2.x `select` API. `create_detail` now uses the existing `repo.get` instead of `db_session.get` as well.

## Why?

Services shouldn't touch the session directly. Detaching objects before `after_commit` still happens in the service, since that's about the webhook timing and not about data access.

## How did you test this?

Only automated tests. `test_bulk_create_details_emits_workout_webhooks` covers the bulk path end to end (records and data sources fetched, one webhook per detail on commit), and the `create_detail` tests cover the single-detail path. Not tested against a live provider sync.

## AI usage

Claude Code (Opus) for the refactor and the PR description.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Event detail creation now retrieves event records and data sources consistently before sending webhooks.
  * Bulk event detail creation handles empty data-source ID sets through the same retrieval flow.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `456b82502fea`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.