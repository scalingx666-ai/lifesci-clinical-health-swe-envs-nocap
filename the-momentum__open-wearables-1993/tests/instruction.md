# Issue

**Title:** feat(backend): persist mobile SDK workout routes and samples

## Description

## What does this change?

The SDK sync already accepted `workouts[].route` and `workouts[].samples` but dropped them. Route points now go to `latitude`, `longitude` and `elevation`, and samples (`heartRate`, `speed`, `cadence`, `power`, which is what the Samsung SDK sends) to the matching series, on the workout's own data source. Unknown sample types and points without a timestamp are skipped.

## Why?

An SDK-recorded run had no GPS track or per-sample heart rate, while the same run from Garmin or Strava had both.

It sits behind `INGEST_WORKOUT_SAMPLES`, like the Garmin and Strava per-sample ingestion, because a 1 h workout is ~10k rows. Points are stored as sent, with no filtering by `horizontalAccuracyM` - cloud providers don't filter either, and there's no threshold to agree on yet.

Overlap with standalone heart rate records: same device and same second upsert into one row (unique key is data source + series + timestamp), otherwise both are kept.

Routes are only usable once #1858 lands - until then coordinates are rounded to ~110 m (#1587).

Updated [coverage](https://docs.openwearables.io/providers/coverage) for Apple, Health Connect and Samsung.

Related issue: #1588

## How did you test this?

Full export from my iPhone (iOS 27.2, Apple Watch history) through the Connect app built with the-momentum/open_wearables_ios_sdk#78, to a local stack with this change and `INGEST_WORKOUT_SAMPLES=true`.

| Source | Workouts | With route |
|---|---|---|
| Apple Watch | 478 | 339 |
| Garmin Connect (writes to HealthKit) | 140 | 0 |

That's 839k `latitude` / `longitude` points and 752k `elevation` (iOS sends a null altitude when CoreLocation marks it invalid). Every outdoor type got a route (walking 176/179, running 101/133, cycling 37/43, hiking 17/17, alpine skiing 7/7) and no indoor one did (strength, squash, stretching: 0). All points sit on the workout's own data source and inside its time range, give or take the 1 s rounding at the edges. Garmin Connect doesn't write `HKWorkoutRoute` to HealthKit, so 0 there is expected.

The export ran in ~1 MB rounds (5 workouts each, the cap from the iOS PR), all 202, and the worker handled them without errors. Before that cap, a single round of a few hundred workouts was 128 MB and got the worker OOM-killed. That's not fixed here: the backend still accepts and holds the whole payload in memory.

Not tested: Samsung / Health Connect payloads from a real device (only the payload shapes), and the coordinates are still at 3 decimals in this run because #1858 isn't in.

## AI usage

Claude Code (Claude Opus 5.5) wrote the implementation and tests; I reviewed the approach and the flag decision.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Workout routes and per-sample measurements can now be stored as time-series data when workout sample ingestion is enabled. Supported data includes location, elevation, heart rate, cadence, speed, and power, depending on the provider.
  * Incomplete or unsupported route points and samples are skipped without preventing the workout from being saved.
* **Documentation**
  * Provider coverage and sync request documentation now describe supported workout route and sample data, including provider-specific availability and structured route and sample fields.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `62f974f971b0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.