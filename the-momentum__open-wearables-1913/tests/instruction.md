# Issue

**Title:** fix(backend): sum Garmin epochs of a slot over their activity types

## Description

## ⚠️ Breaking change

> _Added during review by Sebastian Kalisz._

Intraday Garmin `steps` and `active_energy` samples (`series_sample`, `GET /api/v1/users/{user_id}/timeseries`) rise from the merge on: a slot now carries the sum over its activity types. Days stored before the merge stay understated and are not recomputed, so history is mixed. Daily values from dailies (`series_aggregate`) are unchanged.

| Slot | main | this PR |
|---|---|---|
| `WALKING` 420 steps / 18 kcal + `SEDENTARY` 0 / 0 | 0 steps, 0 kcal | 420 steps, 18 kcal |

## What does this change?

Garmin epochs are summed per 15-minute slot: a slot's steps and active calories are the sum over its activity types, and the epochs of one push are normalized together instead of one by one. An epoch repeated in the same push replaces the earlier one. _(Added during review by Sebastian Kalisz:)_ the replacing epoch also brings its window, offset and `external_id`, so they match the stored value.

## Why?

Garmin sends one epoch per activity type monitored in a slot ("There is one record for each activity type monitored within an individual epoch", Health API docs). Each became its own sample at the slot start, and `series_sample` keeps one row per data source, series type and `recorded_at`, so the last one overwrote the rest. A slot where the user walked and sat was often stored with 0 steps, and intraday steps and active energy came out far below the daily total.

Not covered here: the activity types of one slot sometimes arrive in separate pushes, and the later push still overwrites the earlier sum. Keeping the larger value on conflict would cover it, since a slot's values only grow and Garmin itself keeps the highest step count when it merges data, but that needs a conflict mode in the shared `bulk_create`, so it's left for a follow-up. Days already stored are not repaired; they need a backfill or a replay of the raw payloads.

Related issue: #1912

## How did you test this?

- A slot with `WALKING` (420 steps, 18 kcal) and `SEDENTARY` (0) now goes through `process_items_batch` as 420 steps and 18 kcal; on main it was stored as 0 and 0.
- `normalize_epochs` sums a slot's activity types and counts a repeated epoch of the same type once.
- Full backend suite, `ruff` and `ty` pass.

## AI usage

Claude Code for tracing the epoch flow and first drafts of the fix and tests.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Steps and active calories from different activity types in the same time slot are combined; heart-rate samples remain associated with their respective epochs.
  * When an activity type appears more than once in a time slot, its later record is used.
  * Malformed epochs are skipped individually so other valid epochs can still be processed.
  * Invalid metric values are omitted from totals.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e82dffc9661f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.