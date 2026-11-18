# Issue

**Title:** fix(integrations): Polar exercises are stored 2x the UTC offset in the future

## Description

> **⚠️ Potential breaking change:** no schema change, but on startup the app moves stored Polar workouts to their real time, once per instance (`data_migration`).

Takes over #1679 by @slavarosin (the fork is owned by an organization, so maintainers can't push to its branch), rebased on current `main`.

## What does this change?

Polar sends `start_time` as local time plus `start_time_utc_offset`. We added the offset instead of subtracting it, so Polar workouts were stored twice their offset in the future. The fix flips the sign, and `fix_polar_workout_utc_offset` moves the stored ones.

On top of #1679, the migration:
- reads each connected user's exercise list once (the one the sync reads), not one call per workout, to stay within Polar's rate limit;
- recomputes listed workouts from Polar's JSON, and moves the rest (not listed, inactive connection, 401/403) back by twice their stored `zone_offset`, since the fixed sync can't have written those;
- reads Polar before writing anything, since a token refresh commits the session;
- queues the moved workouts' days for the rollup and refreshes their coverage;
- runs from `app.sh` via `data_migration_service`, before the aggregate backfill.

## Why?

Workouts landed hours late, often on the wrong day. `event_record` is unique on time, not `external_id`, so the fix alone would duplicate every workout Polar still returns; the migration has to run with it.

## How did you test this?

- Unit tests for the sign and every migration path full backend suite
- Synthetic run with Polar's API mocked: 2,000 workouts, 20 users, 0.6s, 20 list calls.
- On our instance, a Polar workout sat 4h after the same session from Apple, Garmin and Google Health; the corrected time matches all three within 20s.

Negative offsets are covered by unit tests only.

## AI usage

Claude Code helped verify the bug against stored data and finish the migration.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Polar workout start and end times are now converted to UTC using the correct timezone offset, improving the accuracy of workout schedules.
  * Existing Polar workout records are corrected during startup when possible. Records without enough timezone information or with conflicting workout times are left unchanged.
  * Updated workout dates are reflected in related daily summaries and data coverage.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d0c021c8dc2d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.