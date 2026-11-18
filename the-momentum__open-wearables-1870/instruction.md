# Issue

**Title:** fix(backend): stop Polar sleep re-syncs from duplicating a night

## Description

> **⚠️ Potential** **Breaking change:** no schema change, but on startup the app rewrites stored Polar sleep (only instances with Polar connected). It removes duplicated stage intervals, resets time in bed and, for nights without stages, the sleep and stage minutes, and sets `external_id` on existing Polar nights. It runs once per instance (recorded in `data_migration`).

## What does this change?

Polar sleep now gets `external_id = "sleep-<date>"`, so a re-sync replaces the night instead of merging into it. A new data migration, `dedupe_polar_sleep`, repairs the nights stored before the fix. Polar sleep without a date is skipped, like sleep without a start or end time.

## Why?

Polar has no sleep id: its API keys each night by date (`/v3/users/sleep/{date}`). Without an `external_id`, every re-sync of a night inside the sync window went through the adjacent-session merge, which appended another copy of the stage timeline and added the time in bed again. Nights without stages also had their sleep and stage minutes added up. Every other provider that writes sleep already passes an id, which is why only Polar showed this.

The fix stays in the provider rather than the merge: the merge is right for adjacent sessions, the problem was Polar re-entering it for the same night. Ultrahuman keys its sleep the same way (`sleep-<date>`).

The migration runs once per instance through `data_migration_service`. It keeps one copy of each stage interval, resets time in bed to the session length, divides the minutes of nights without stages by the number of copies, and sets the external id from the local wake-up date (Polar sleep has no `zone_offset`, so the offset comes from the stage timestamps). It reads nights in batches and skips and reports a night it can't read instead of failing.

Not covered: internal sleep scores of repaired nights aren't recomputed, and a night without stages is keyed by the UTC date of its end, which is a day early well east of UTC (there a re-sync merges as before).

Related issue: #1539

## How did you test this?

* Regression test: three syncs of the same night through `_save_sleep` keep one copy; it fails without the fix.
* Migration tests: duplicated stages, minutes of nights without stages, wake-up date in UTC+10 and right before midnight, an unreadable night, batching, other providers untouched, dry run, second run.
* Local instance: wrote nights through the pre-fix merge path (with stages, without stages, one corrupted), restarted the app and checked that the startup run repaired them, skipped the corrupted one, recorded itself and skipped on the next start, and that a later re-sync replaces the repaired night.
* Confirmed on a raw Polar API payload that `date` is the local wake-up date: a night that started at 23:49 on one day and ended the next morning is dated by the day it ended.

## AI usage

Claude Code was used to propose the fix and implement the tests and help write this PR description.

## Summary by CodeRabbit

* **Bug Fixes**
  * Polar sleep records are matched to their sleep date, helping prevent repeated imports from creating duplicate nights.
  * Records missing a required date or start or end time are skipped.
  * Duplicate sleep stages and inflated time-in-bed totals are corrected. Existing sleep records with available stages are associated with the local wake-up date.
  * Sleep data repairs run during startup; unreadable records are skipped, and startup continues if the repair encounters an issue.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Polar sleep records are now identified consistently by sleep date, preventing repeated syncs from creating duplicate entries.
  * Duplicate sleep data is corrected, including repeated sleep stages and inflated time-in-bed or sleep-duration values.
  * Records missing a date or sleep start or end time are skipped instead of being saved.
  * Existing Polar sleep data is checked and repaired automatically during startup. If the check cannot complete, it will be retried on a later startup.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `95223ea6bba9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.