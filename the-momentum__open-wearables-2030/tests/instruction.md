# Issue

**Title:** feat: Add Sync Status endpoint for SDK

## Description

Adds `GET /api/v1/sdk/users/{user_id}/sync/status?provider={slug}`, which returns where a user's SDK sync for one provider stands. The backend becomes the source of truth for sync progress, and the device's local state becomes a cache. After a logout wipes local state, the SDK can restore it from here
instead of starting over.

## Response

```json
{
  "provider": "apple",
  "historicalSyncCompleted": false,
  "syncedUntil": "2026-11-02T11:12:24Z",
  "dataTypes": [
    {
      "type": "heart_rate",
      "kind": "series",
      "historicalSyncCompleted": false,
      "lastSyncedAt": "2026-11-02T11:29:44.785760Z",
      "coveredRange": { "startDate": "2026-06-25T13:12:31Z", "endDate": "2026-11-02T11:12:24Z" }
    }
  ]
}
```

- `historicalSyncCompleted`: true when an SDK historical export finished every data type it reported, and false when an export exists but hasn't finished. null when there's no historical export on record: either nothing has synced yet, or the SDK version doesn't send `syncSessionId`, so the server can't tell.
- `syncedUntil`: the newest data held from the provider, which is where live sync continues from. null when nothing has synced yet.
- `dataTypes[]`: one entry per type held, from data_type_coverage:
  - `coveredRange`: earliest and latest data held for the type. Both SDKs export newest first, round-robin across types, so an unfinished type resumes backwards from `coveredRange.startDate`.
  - `lastSyncedAt`: `data_type_coverage.last_written_at`, i.e. when an upload last touched the type.
  - `historicalSyncCompleted`: same meaning per type. null when no export reported the type.
- New user: 200 with the empty state (null / null / []), not 404.
- Errors: 400 for an unsupported provider, 403 when the SDK token belongs to another user, 404 for an unknown user. google is accepted and returned as health_connect.

## Changes during review

> _Added during review by Sebastian Kalisz._

- `dataTypes[].exportedRange` (new, nullable): what the latest historical export has sent of the type so far, taken from the batches' sample times. An unfinished type resumes backwards from `exportedRange.startDate`. `coveredRange` stays the span of all data held, but it is no longer the resume point: gaps inside it are invisible and retention moves its start.
- A series filled only from workout statistics, samples or routes (e.g. `weather_temperature`) no longer gets a row in a historical run. The device sends no end event for it, so any export with an outdoor workout stayed unfinished forever.
- SDK logs normalize the provider like uploads do (`google` → `health_connect`), so the run opened by the start log is found under the canonical slug.
- `lastSyncedAt` for data held before coverage was tracked is the newest sample's time, not the upload time.
- The route lists no error responses, like the other routes.

Not fixed: an export can read as finished while batches of a type with no row yet are still queued. The start log cannot close this gap, because its `dataTypeCounts` holds records already sent (0 on a fresh export) and the device sends no end event for a type with nothing to send. Closing it needs an SDK change.

## Breaking change

> _Added during review by Sebastian Kalisz._

No API field is removed. Two behaviour changes for SDK historical runs:

- Outgoing data-type webhook: `written` was always `null` for SDK exports and now carries `{"start", "end"}` of the samples the export's batches wrote.
- Run breakdown (`/sync/history`): series filled only from workouts are no longer listed for historical SDK runs.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

- **New Features**
  - Added an SDK sync-status endpoint that reports historical sync progress, the latest synced time, and per-data-type completion and date coverage.
  - Sync status is available by provider and reflects prior sync activity, including interrupted or failed exports. Users with no sync history receive an empty status.
  - Per-data-type status includes the date range covered by the latest historical export, helping identify where an unfinished export can resume.
- **Documentation**
  - Added the sync-status endpoint, response details, and possible error responses to the API reference.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `30470f4f4a53`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.