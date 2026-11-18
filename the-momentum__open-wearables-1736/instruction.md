# Issue

**Title:** fix(backend): declare Samsung coverage from what the SDK actually emits

## Description

## What does this change?

Samsung's coverage is now declared explicitly from what the Android SDK's `SamsungHealthManager` emits, instead of reusing the full Android/Health Connect metric map and Apple's workout fields. The Samsung column loses 13 timeseries and 4 workout fields it never delivered:

- `resting_heart_rate`, `heart_rate_variability_rmssd`, `respiratory_rate`, `distance_walking_running` - no such Samsung data type / not read by the SDK
- `power`, `speed` - only present in workout `log` samples, which the backend doesn't ingest
- `average_met`, `running_*` (3), `swimming_stroke_count`, `weather_*` (2) - HealthKit-only workout statistics
- workout fields `steps_count` (Samsung sends `count`, not `stepCount`), `average_cadence` (`meanCadence` goes to the `cadence` series), `entry_source` (SDK sends no `recordingMethod`), `moving_time_seconds` (nothing sets it)

## Why?

Users saw empty series and `avg_hrv_rmssd_ms: null` for things the matrix advertised. The Samsung Health Data SDK is much narrower than Health Connect:

- [`DataTypes`](https://developer.samsung.com/health/data/api-reference/-shd/com.samsung.android.sdk.health.data.request/-data-types/index.html) has no resting HR, HRV or respiratory rate type
- [`HeartRateType`](https://developer.samsung.com/health/data/api-reference/-shd/com.samsung.android.sdk.health.data.request/-data-type/-heart-rate-type/index.html) / [`HeartRate`](https://developer.samsung.com/health/data/api-reference/-shd/com.samsung.android.sdk.health.data.data.entries/-heart-rate/index.html) expose only bpm/min/max, with no IBI to derive HRV from
- [`SleepType`](https://developer.samsung.com/health/data/api-reference/-shd/com.samsung.android.sdk.health.data.request/-data-type/-sleep-type/index.html) carries no HRV; [`EnergyScoreType`](https://developer.samsung.com/health/data/api-reference/-shd/com.samsung.android.sdk.health.data.request/-data-type/-energy-score-type/index.html) returns only the score
- [`ExerciseSession`](https://developer.samsung.com/health/data/api-reference/-shd/com.samsung.android.sdk.health.data.data.entries/-exercise-session/index.html) has none of the HealthKit running/swimming/weather statistics

Same approach as #1233 (Apple RMSSD), taken one step further: an explicit Samsung allowlist rather than subtracting from the Android map, so a new Health Connect type doesn't silently show up for Samsung. The coverage guard test gets a Samsung exception for detail fields the shared import code can set, but only from inputs Samsung never sends. Gaps that are fixable on the SDK/backend side (step count, cadence, power, sleep score, etc.) are tracked in separate issues.

Related issue: #1723

## How did you test this?

- `uv run pytest tests/providers/test_provider_coverage.py` - 59 passed
- Regenerated `docs/providers/coverage.mdx`; diffed the Samsung column against `main`: exactly the 17 entries above removed, nothing added
- Each remaining entry traced to an emit in `SamsungHealthManager.kt` or a key in the backend workout-statistic maps

Not tested against a real Galaxy Watch sync; this touches the coverage declaration only, not ingestion.

## AI usage

Claude Code - checked the Samsung SDK docs, traced SDK and backend code, made the change, drafted this description.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Data Coverage**
  * Samsung coverage now reflects the metrics and workout details available from Samsung Health. HRV, resting heart rate, respiratory rate, several distance, movement, swimming, power, speed, and weather metrics are marked unsupported, as are workout cadence, entry source, moving time, and step count.
  * Step count is also marked unsupported for Sensorbio.
* **Documentation**
  * Updated the provider coverage matrix to reflect these support changes.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7331311b7cec`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.