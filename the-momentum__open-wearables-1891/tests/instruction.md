# Issue

**Title:** perf(integrations): skip Strava stream fetch when workout samples already exist (#1298 follow-up)

## Description

Supersedes #1298 by @slavarosin. The fork is org-owned, so maintainer pushes aren't possible; the original commit is kept.

On top of it:
- merged main
- scoped the existing-samples check to the recording device (`device_name`), so overlapping activities from different devices don't block each other's streams
- trimmed the comment in `_ingest_workout_streams`

Another change - also merging #1447 here.

1447 adds retry in case webhooks arrive before stream processing (which would cause Strava to return empty samples), with exponential backoff.

My changes on top of those:
- trimmed comments, again
- registering the new celery task and logic associated with it
- updating setting to make this backoff more configurable

_(Added during review by Sebastian Kalisz:)_
- The check for stored streams looks only at Strava's stream series types, so it reads the workout's window instead of the device's whole history, and it runs once per workout. A failed check is logged and the streams are fetched as before.
- A retry is scheduled only when Strava returned no streams, and never for a manual activity, which gets none. The retry task reschedules only after an outage or a database error, not after a deleted activity (404), a lost connection or a request Strava rejected.

## Behavior changes

_(Added during review by Sebastian Kalisz:)_
- Stored streams are not fetched again: an activity cropped in Strava keeps its earlier samples.
- A Strava `update` event no longer sends the workout webhook again, since the workout's detail already exists.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Strava workout imports now avoid fetching streams when matching samples are already stored, reducing unnecessary repeat processing.
  * When an activity has no stream data yet, the app can retry fetching it later, with increasing delays and a limit on retry attempts.
  * Empty stream results are now reported consistently, and retries stop for activities that cannot be retrieved or are not eligible.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c8b98beaf577`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.