# Issue

**Title:** feat: Backfill only the gap since last sync on reconnect

## Description

On reconnect, historical sync was always dispatched with a fixed 90 day (or 30 for Garmin) window. The OAuth callback stamped `last_synced_at = now` before anythin read it, so the boundary was lost and every subsequent reconnect asked for the full range. For most providers it was just redundant calls, but Garmin returns a 409 when asking for a gap that was already provided with webhooks.

How the gap is chosen now:
- Old `last_synced_at` (before connection broke) is used, but only if `data_type_coverage` holds something for that provider (as a sanity check). A purge removes coverage but keeps the connection row, so otherwise a purge+reconnect would skip the historical backfill.
- For pull sync -  (last stamp - pull_sync_lookback), but never earlier than the 90 days as before.
- Garmin - no lookback, and never before the latest accepted window in `sync_run`

At first I thought that something like `min(coverage_end)` from the data type coverage table would help, but thinking about it, some slow changing data types could skew the results here and not affect the lookback at all, and a more consistent per-data type "asked up to" would require persisting live runs which is off by default and costly, but this approach is still good IMO.



<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

## Summary

* **New Features**
  * Reconnecting an integration can backfill data from the previous sync point, while respecting existing coverage and the configured historical lookback.
  * New connections can retrieve historical data within the available lookback period.
  * Garmin reconnects resume from the appropriate point after previously requested backfills and skip requests when no time range remains.

* **Bug Fixes**
  * Improved backfill date-range handling for more consistent syncs, including retries when a requested range is shortened.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fed9328b1bb8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.