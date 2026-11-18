# Issue

**Title:** fix: add `sleep_session` type to GH API sleep records

## Description

## ⚠️ Breaking change

> _Added during review by Sebastian Kalisz._

API and webhook consumers holding Google Health sleep ids: Google sessions less than 120 min apart now merge in `create_or_merge_sleep` into one record with a **new id** and `is_nap: false`; the earlier record is deleted.

`sleep.created` — a nap 07:30–08:00 arriving after a stored night 23:00–06:30 (derived from code):

```diff
- {"id": "c41d…", "start_time": "…T07:30:00+00:00", "end_time": "…T08:00:00+00:00", "is_nap": true}
+ {"id": "e07a…", "start_time": "…T23:00:00+00:00", "end_time": "…T08:00:00+00:00", "is_nap": false}
```

## What does this change?

- Google Health sleep rows are saved with `type = "sleep_session"`, so `find_adjacent_sleep_record` finds a stored night.
- Re-fetching the same night no longer sends `sleep.created` again with the old details; it replaces the details (stages included) in place, without a webhook.
- `backfill_google_sleep_type.py` types existing untyped Google sleep rows, in batches of Google sources, once per instance (`data_migration`).

| Re-fetch of a stored Google night | Before | After |
|---|---|---|
| `sleep.created` | sent every sync, old details | not sent |
| `GET /api/v1/users/{user_id}/events/sleep` | first details kept | latest details |

## Why?

The handler left `type` NULL, so a stored Google night was never matched: the insert hit the existing row and re-sent `sleep.created` with stale data, and a night whose window shifted was stored twice.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Google Health sleep sessions are now consistently categorized, including sessions imported before this update.
  * Sleep records can be updated with sleep-stage details when those details become available, keeping session information current.
  * Previously untyped Google Health sleep records are corrected automatically. Processing is batched, and a failed attempt can be retried on a later startup.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `66a3288033f8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.