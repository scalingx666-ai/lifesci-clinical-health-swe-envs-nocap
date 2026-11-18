# Issue

**Title:** feat(backend): store Health Connect moderate and vigorous minutes as exercise time

## Description

## What does this change?

Health Connect `ActivityIntensityRecord` arrives from the SDK as two metric types. Both are stored as `exercise_time` (minutes); the minutes are the record's length, `value` and `unit` are ignored.

| SDK type | Series | Value |
|---|---|---|
| `ACTIVITY_INTENSITY_MODERATE` | `exercise_time` | `(endDate - startDate)` in minutes |
| `ACTIVITY_INTENSITY_VIGOROUS` | `exercise_time` | `(endDate - startDate)` in minutes |

A record whose `endDate` is not after `startDate` is reported as dropped. Upload from the SDK (`POST /api/v1/sdk/users/{user_id}/sync`), derived from code:

```json
{"type": "ACTIVITY_INTENSITY_VIGOROUS", "startDate": "2025-04-10T10:00:00Z", "endDate": "2025-04-10T10:25:00Z", "value": 0, "unit": "min"}
```

→ `series_sample`: `exercise_time = 25`.

A moderate and a vigorous record from the same source with the same start share one sample key; the later one in the batch overwrites the earlier.

## Why?

Health Connect has no exercise-minutes record; intensity records are its equivalent of Apple's exercise time. Needs the Android SDK change that sends these types, merged together with it.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Health Connect now supports moderate and vigorous activity records for exercise-time tracking, with duration calculated from the recorded start and end times.
* **Bug Fixes**
  * Activity records with empty or reversed time intervals are rejected.
* **Documentation**
  * Updated provider coverage information: Health Connect is marked as supported for exercise time, and Oura is marked as unavailable.
  * Clarified that activity-intensity durations are calculated from timestamps; the supplied value and unit are ignored.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7702bd9e9e43`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.