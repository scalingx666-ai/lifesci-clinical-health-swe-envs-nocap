# Issue

**Title:** feat(backend): store intraday activity samples for Polar and Withings

## Description

## What does this change?

Polar and Withings now store per-minute activity samples next to their daily totals (Polar: steps; Withings: steps, distance, active energy). No backfill: samples appear as ranges are synced.



## Why?

Polar already returned these samples - `/v3/users/activities` is requested with `steps=true` - but the normalizer ignored them. Withings needs `getintradayactivity`, which returns at most 24h per call, so one request goes out per day that has a daily row. Slices relayed from other platforms (`model_id` 1000 and above) are dropped.

A series row is keyed by its instant alone, and Polar's first sample lands on `start_time`, where the daily total is stored, so the sample overwrote the total with zero. Both providers now skip a sample on the daily total's instant.

## How did you test this?

Unit tests, full suite. Polar: normalizer run over stored responses, daily totals intact. Withings: demo account synced locally, samples sum to the daily totals and a re-sync is idempotent. The demo data is synthetic, so real density is untested.

## Worth knowing

- Polar timestamps are naive local, Withings samples UTC with an offset.
- These providers now feed `sedentary_minutes`, which reads low because samples do not cover every worn minute, and may win source ranking on hourly charts.
- Large Withings backfills can still hit the throttle (#1724).

## AI usage

Claude Code for reading the provider specs, drafting the implementation and tests, and reviewing the branch.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Withings syncing now includes timestamped intraday steps, distance, and active calories alongside daily activity totals.
  * Polar activity data now includes timestamped intraday step samples, kept distinct from daily totals.
* **Documentation**
  * Provider integration guides now describe the available intraday activity data: timestamped steps for Polar and timestamped steps, distance, and active calories for Withings.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `58dc419a4f5c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.