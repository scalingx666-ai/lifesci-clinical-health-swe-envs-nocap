# Issue

**Title:** fix(backend): save an Apple Watch night soon after its upload

## Description

## What does this change?

An Apple Watch night is saved 15 minutes after the last upload that added to it (`SLEEP_UPLOAD_QUIET_MINUTES`) instead of 2 hours after its last sample, and `finalize_stale_sleeps` runs every 5 minutes instead of every hour.

The quiet period applies per open session. Since #1876 each writer app has its own session (Apple Watch and iPhone count as one writer), so it only applies to the Apple session once it holds Apple Watch sleep, and only that session's uploads restart it.

## Why?

An SDK night was saved 2 hours after its last sample, plus up to an hour until the next task run, so a watch night uploaded right after waking reached the API and the sleep score up to 3 hours later.

The watch writes the whole night to HealthKit after waking and the SDK usually sends it within seconds, so a short quiet period is enough. Other apps writing to HealthKit (Garmin Connect, Oura) can send a night over syncs hours apart, so their sessions keep the 2 hour gap, and their uploads do not hold back the watch night. A piece that arrives after its night was saved is still merged into it by `finish_sleep`.

The finalize task also drops users with no open session left (their Redis state expired) from the set it scans, so the more frequent run does not keep checking them.

The rest of the delay in #1319 happens before the upload (iOS decides when the watch syncs with the phone and when the app runs in the background), so this is only part of it.

Related issue: #1319

## How did you test this?

- `uv run pytest`: all passed, including tests for the closing rule, the per-writer quiet period and the task.
- A fake-clock simulation (not part of this PR) that feeds uploads at chosen times through `handle_sleep_data` and `finalize_stale_sleeps` on a local stack (Postgres and Redis). It ran before #1876 was merged, so "main" below is main without per-writer sessions. Night from 23:00 to 07:00:

| Scenario | Saved on main | Saved on this branch |
|---|---|---|
| Watch night uploaded at 07:10 | 09:00 | 07:25 |
| Same night in two uploads, 07:10 and 07:24 | 09:00 | 07:40 |
| Garmin night via HealthKit (ends 07:05) uploaded at 07:30 | 10:00 | 09:05 |
| iPhone in-bed sample and watch night in one upload at 07:10 | 10:00 | 07:25 |
| Watch night uploaded at 14:00 | 14:00 | 14:00 |
| Watch at 07:10, Oura app writes the night at 08:00 | one session mixing both, awake time lost | a watch session and an Oura session |

  Apart from the last row, the stored sessions are the same on both branches. Current main already gives two sessions in the last row.
- End to end through the SDK sync endpoint with `SLEEP_UPLOAD_QUIET_MINUTES=1` and `SLEEP_SYNC_INTERVAL_SECONDS=60`: a watch night was saved within 150 s, an Oura night stayed open.

Not tested on a real device.

## AI usage

Claude Code for tracing the sync flow, preparing the simulation, and first drafts of the tests and doc

## Breaking change

None in the API. The default `SLEEP_SYNC_INTERVAL_SECONDS` goes from 3600 to 300, so instances without an override run `finalize_stale_sleeps` every 5 minutes after upgrading; set it to 3600 to keep the hourly run.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Apple Watch sleep sessions can be finalized after 15 minutes without new uploads; other sessions are finalized based on time since sleep ended.
  * Sleep sessions are checked every five minutes.
  * Sleep data from different sources is kept separate, while late samples from the same source can be merged.
* **Documentation**
  * Added guidance on Apple Health data availability, session timing, and scoring timelines.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a6732845951`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.