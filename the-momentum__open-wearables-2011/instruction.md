# Issue

**Title:** fix(backend): keep the day's highest Garmin body battery peak

## Description

## What does this change?

Garmin body battery scores keep the highest value of all stressDetails pushes of their day
instead of the first one. A run-once data migration raises the stored scores to the highest
sample of their day.

_(Added during review by Sebastian Kalisz:)_ Days whose samples retention already deleted keep their current score. A sample keeps the latest value Garmin pushed for its timestamp, so a peak Garmin later revised down is not restored: the score rises only to what the samples still hold.

## Why?

Garmin resends a day's stressDetails after every sync, but the score was inserted with
`ON CONFLICT DO NOTHING`, so it kept the first push's peak, usually from the hours after
midnight.

The upsert keeps the greater value rather than the latest one. In our instance's raw payloads
Garmin resends most days many times, sometimes out of order, and occasionally revises single
values downward, but never a day's peak, so the greater value is the rule that doesn't depend
on processing order. Other scores keep `DO NOTHING`. Garmin's daily stress average likely has
the same first-push problem, but it needs "latest wins", so it's left for a follow-up.

The migration takes a score's day up to the user's next body battery score, so 23- and 25-hour
days and time zone changes don't pull in the next day's samples.

The upsert targets the score's unique key, data_source_id from #1877 included.

No breaking change: body battery scores now hold the day's peak, as the category describes.

Fixes: #2001

## How did you test this?

- Unit tests for the upsert, for `process_items_batch` (the path webhooks and backfills take)
  and for the migration, including a test that fails on `main`.
- Replayed real stressDetails payloads from our instance through `process_items_batch`, in
  arrival and in reverse order: every day ends at its peak. With `main`'s ingestion, then the
  migration, the low days are raised to their peak, never above it, and a second run changes
  nothing. The replay covers 23- and 25-hour days, a day sent twice in one batch, pushes
  arriving out of order and values revised downward.
- Not run against live webhooks.

## AI usage

Claude Code helped outline the problem, write the tests and helped write this PR

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Garmin Body Battery scores now retain the highest reading for each scoring period, even when readings arrive out of order or in the same batch.
  * Existing scores are raised when a higher matching Garmin reading is available. Scores are never lowered, and data from other providers is unaffected.
  * Historical scores are updated automatically when a matching sample exceeds the stored score. Periods without a higher sample remain unchanged.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a401845bc5c3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.