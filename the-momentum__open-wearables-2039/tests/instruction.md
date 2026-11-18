# Issue

**Title:** feat: Recovery summary for providers other than Whoop

## Description

**Breaking changes for public API**

- Cursors from before this change are rejected (invalid cursor): the format changed from score timestamp/id to date/source/device.
- `source.provider` is now the device's provider, not the scoring provider (`internal` -> `garmin`).
- A day without a recovery score now returns a row, with `recovery_score: null`.
- _(Added during review by Sebastian Kalisz)_ A recovery score is dated by its local day (`recorded_at` at its `zone_offset`), like the vitals and the sleep it is merged with; before, by its UTC date. A score recorded late in the evening west of UTC, or after midnight east of it, moves to a neighbouring date.
- _(Added during review by Sebastian Kalisz)_ A field the winning source lacks is taken from the next-ranked source that has it (`fill`, as in the activity summary on #2020), while `source` still names the winner.

---

This PR is stacked on top of stack #2023, but not necessarily because of its logical connection to it - it's mostly because of the priority filtering mechanisms on summaries. I didn't want to introduce merge conflicts after merging any one of the two branches, so the lower 3 can be merged independently, and this can be left on top afterwards.

## What does this change?

`GET /summaries/recovery` now builds each day from the stored series instead of from `HealthScore(RECOVERY)` rows: resting HR, HRV (SDNN and RMSSD) and SpO2 come from the day and night aggregates, sleep duration and efficiency from the main sleep, and a recovery score is merged in where one exists. Any provider with the underlying data now gets rows, not just WHOOP.

## Why?

Rows came only from recovery-score records, and the metrics were read from those records' `components` under WHOOP's key names. A Garmin, Oura or Apple user with months of resting HR and HRV got an empty list. Since 2026-10-29 the internal recovery scores produce rows, but every metric in them is null: their components are sub-scores keyed `hrv` / `rhr` / `sleep`. On prod, the same Garmin day goes from this (example data):

| | before | after |
|---|---|---|
| `source.provider` | `internal` | `garmin` |
| `resting_heart_rate_bpm` | null | 43 |
| `avg_hrv_rmssd_ms` | null | 82.0 |
| `avg_spo2_percent` | null | 95.5 |
| `sleep_duration_seconds` | null | 30720 |
| `sleep_efficiency_percent` | null | 96.6 |
| `recovery_score` | 64 | 64 |

The vitals use the same reads as the body summary's averages (`day_values`, split out of `period_averages`). That means the provider's day row first, then the value on the night's sleep, then samples. Through #2024 they also recount days the rollup hasn't caught up with. Paging reuses the activity summary's day-window paging, renamed `_page_days`, and its date/source/device cursor. One source wins per date via `_filter_by_priority`, as in activity.

Not done: filling a winning row's gaps from the next-ranked source (`fill`, as activity does on #2020). It would make `source` name a device that didn't supply every field, so it's left for a separate decision.

_(Added during review by Sebastian Kalisz)_ Superseded by 3a13a815: the recovery summary now uses `fill` (see the breaking changes above).

Example JSON response from the endpoints (adjusted, so not real data):

Apple, no score:
```json
{
  "date": "2026-10-24",
  "source": { "provider": "apple", "source": "apple", "device": "Apple Watch Series 6", "device_type": "watch" },
  "sleep_duration_seconds": 35880,
  "sleep_efficiency_percent": 91.7,
  "resting_heart_rate_bpm": 67,
  "avg_hrv_sdnn_ms": 56.0,
  "avg_hrv_rmssd_ms": null,
  "avg_spo2_percent": 98.0,
  "recovery_score": null
}
```

WHOOP, score from a record without a data source, RMSSD from its components:
```json
{
  "date": "2026-10-24",
  "source": { "provider": "whoop", "source": "whoop", "device": "WHOOP 3.0", "device_type": "band" },
  "sleep_duration_seconds": 35880,
  "sleep_efficiency_percent": 91.7,
  "resting_heart_rate_bpm": 52,
  "avg_hrv_sdnn_ms": 61.0,
  "avg_hrv_rmssd_ms": 24.4,
  "avg_spo2_percent": 96.0,
  "recovery_score": 41
}
```

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Recovery summaries now include available daily health metrics and main-sleep data across supported providers. They use the highest-priority source for each day and can fill missing metric groups from other sources.
  * Recovery scores appear only when a provider reports a score.
* **Documentation**
  * Updated recovery-summary guidance to describe provider coverage and clarify the SDNN and RMSSD heart-rate variability metrics.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f3d2e574977a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.