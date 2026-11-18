# Issue

**Title:** feat(backend): store mobile SDK workout laps and segments

## Description

## What does this change?

Mobile SDK workout `laps` and `segments` are now stored in `workout_details.segments`, in the shape the FIT parser already stores for Garmin, so `/workouts?include=segments` returns the same JSON for Apple, Health Connect and Garmin. No migration.

- pool-swim laps (stroke style or SWOLF present) -> `kind: length` with `swim_stroke`, `total_strokes`, `swolf`, `avg_speed`, `length_type: active`; kickboard maps to `drill`, as in the FIT enum
- other laps -> `kind: lap` with `distance_meters`, `avg_speed`
- HealthKit segment events and Health Connect exercise segments -> `kind: split` (`split_type`, `repetitions`); HealthKit markers are dropped

_(Added during review by Sebastian Kalisz:)_ Only newly imported workouts get segments. A workout already stored is skipped on a re-send together with its details, as for every other detail field, so workouts imported before this change, or sent again by a full resync, keep no segments.

## Why?

Apple Watch pool swims arrived as distance + total strokes only, although iOS SDK 0.15.0+ already sends every `HKWorkoutEvent` in `laps`. Stroke style and SWOLF are read from typed `strokeStyle` / `swolf` lap fields (companion PR: the-momentum/open_wearables_ios_sdk#79) and fall back to the stringified `HKSwimmingStrokeStyle` / `HKSWOLFScore` metadata that released SDK builds send, so existing apps get stroke style without an SDK upgrade.

Per-length stroke count is not in HealthKit event metadata (it lives in `swimmingStrokeCount` samples), so `total_strokes` is only filled when an SDK sends `strokeCount`; no SDK does yet. `swolf` is an extra key the FIT shape does not have.

Related issue: #1596

## How did you test this?

- `uv run pytest` in `backend/` (testcontainers Postgres): 3585 passed. New: `tests/services/test_sdk_workout_segments.py` (typed fields, stringified metadata, kickboard, unknown stroke, running laps + segment events + markers, Health Connect segments) and an import test asserting the stored `segments` JSON.
- `test_provider_coverage`: `segments` declared for Apple / Health Connect, marked unreachable for Samsung (it sends no laps); coverage docs and `docs/openapi.json` regenerated.
- Not tested against a real Apple Watch swim payload yet.

## AI usage

Claude Code (Claude Opus 5.5) wrote the code and tests from the issue analysis; I reviewed the result.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Workout imports now include structured lap and segment details, such as timing, distance, repetitions, and segment type. Swimming laps can include stroke style, stroke count, SWOLF, and speed metrics.
  * Workout segments are supported for Apple, Garmin, and Health Connect.
* **Bug Fixes**
  * Invalid lap or segment entries no longer prevent other valid workout details from being imported.
* **Documentation**
  * API documentation now describes the fields accepted for workout laps and segments.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1204faa2a7dc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.