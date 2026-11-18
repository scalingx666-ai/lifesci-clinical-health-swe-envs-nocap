# Issue

**Title:** fix(backend): skip Strava streams for manual activities

## Description

## What does this change?

Strava workouts no longer request `/activities/{id}/streams` for a manual activity. A manual activity never has streams, so Strava answers 404 on every sync that re-covers it, and each answer left two error log lines: "API error" from `api_client` and "Failed to fetch Strava workout streams" from `_ingest_workout_streams`. The stored-streams probe is skipped for it too.

The webhook path already skipped the stream retry for manual activities; that check now lives in `_ingest_workout_streams`, so `process_push_activity` drops its own `not activity.manual`.

Reported in #1680 by @slavarosin.

## How did you test this?

- New test: a manual activity makes neither the probe nor the streams request.
- `tests/providers/strava` passes, `pre-commit run --all-files` is clean.

## Breaking change

None.
<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Manual Strava activities are no longer checked for workout samples or retried when stream data is unavailable, preventing unnecessary data requests.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9021a99c06d9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.