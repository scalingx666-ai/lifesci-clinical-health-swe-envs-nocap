# Issue

**Title:** feat(api): aggregates: workout statistics

## Description

## ⚠️ Breaking change

Response shapes are unchanged; some values change.

| Field | Before | After |
|---|---|---|
| `/events/workouts` statistics a provider did not send | `null`, except `avg_heart_rate_bpm` | ours from the workout's own samples (heart rate min/max, steps, power, cadence, …) |
| `/events/workouts` `calories_kcal` without a provider figure | `null` | the workout's own active energy samples added up |
| `/events/workouts` `elevation_gain_meters`, `calories_kcal` when the provider sent `0` | `null` | `0.0` |
| `/events/workouts/totals`, `/summaries/activity` workout energy, distance, elevation | the provider's figures only | per workout the provider's, else ours |

## What does this change?

Workouts read their statistics from `event_record_aggregate`; `workout_details` keeps only what is not a series statistic, and `energy_burned` for providers whose energy series is not established yet.

```mermaid
%%{init: {"flowchart": {"htmlLabels": false}}}%%
flowchart TB
    subgraph stat["every statistic"]
        direction LR
        p1[("event_record_aggregate<br/>computed_by = provider")] -- "missing" --> o1[("event_record_aggregate<br/>computed_by = open_wearables<br/>rolled up from the workout's samples")]
    end
    subgraph hr["avg_heart_rate_bpm, one more step"]
        direction LR
        p2["provider"] -- "missing" --> o2["ours"] -- "missing" --> s2["samples of the same app's<br/>other sources"]
    end
    subgraph cal["calories_kcal"]
        direction LR
        p3["provider, in its declared series<br/>total_energy or active_energy"] -- "missing" --> c3["workout_details.energy_burned<br/>(undeclared providers)"] -- "missing" --> o3["ours<br/>active_energy samples summed"]
    end
    stat ~~~ hr ~~~ cal
    classDef new fill:#eaf2fb,stroke:#1f618d,color:#000
    classDef old fill:#f4f4f4,stroke:#7f8c8d,color:#000
    class p1,o1,p2,o2,p3,o3 new
    class s2,c3 old
```

| Field | Source (`event_record_repository.py:get_workout_statistics`, `workout_energy`) | Series | Statistic |
|---|---|---|---|
| `avg_heart_rate_bpm` | provider, else ours, else samples of the same app's other sources | `heart_rate` | `avg` |
| `max_heart_rate_bpm`, `heart_rate_min` | provider, else ours | `heart_rate` | `max`, `min` |
| `steps_count` | provider, else ours | `steps` | `sum` |
| `distance_meters`, `avg_pace_sec_per_km` | provider, else ours | `distance` | `sum` |
| `average_speed`, `max_speed` | provider, else ours | `speed` | `avg`, `max` |
| `average_watts`, `max_watts` | provider, else ours | `power` | `avg`, `max` |
| `average_cadence` | provider, else ours | `cadence` | `avg` |
| `elev_low`, `elev_high` | provider, else ours | `elevation` | `min`, `max` |
| `elevation_gain_meters` | provider, else ours | `elevation_gain` | `sum` |
| `calories_kcal` | provider in its declared series → `workout_details.energy_burned` → ours | `total_energy`, `active_energy` | `sum` |
| `/events/workouts/totals` energy, distance | the same, summed in SQL | | |
| `/summaries/activity` `elevation_meters` | provider, else ours | `elevation_gain` | `sum` |

The mapping is `WORKOUT_DETAIL_STATS`, the one the save path writes with, read the other way round.

Series webhooks gain `window_seconds` on every sample, as `/timeseries` did; the workout webhook keeps sending the values it was saved with.

## Why?

| Decision | Because |
|---|---|
| calories: declared series, then the column, then ours | a provider's own figure stays what clients saw; ours only fills workouts that had none |
| the column stays for undeclared energy | Oura, Polar, Suunto, Strava, Fitbit, SensorBio and Samsung workout energy has no established series yet (listed in the ingestion PR) |
| avg heart rate still falls back to the same app's other sources | our session row covers the workout's own source only |

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Improvements**
  * Workout responses now use aggregated statistics for distance, pace, heart rate, elevation, steps, speed, cadence, and power.
  * Calorie totals draw on available provider and workout data, while average heart rate is rounded consistently.
* **New Features**
  * Timeseries webhook samples now include `window_seconds`, showing the reporting-window duration or `null` for instant readings.
* **Documentation**
  * Webhook guidance explains `window_seconds` and provides examples for timed and instant readings.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d96ad13fe996`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.