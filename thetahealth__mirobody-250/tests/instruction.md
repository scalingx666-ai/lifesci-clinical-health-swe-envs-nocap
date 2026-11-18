# Issue

**Title:** catalog: every series a decoder writes declares a daily statistic

## Description

.

### What was wrong

A series becomes a daily reading only through the statistics its catalogue row declares: `standardize/aggregate/rule_generator.py` skips a SERIES metric whose `aggregation_methods` is empty. 22 of the series metrics the device decoders write declared none. They were decoded and stored in `series_data`, then shown nowhere: not in the indicator list, the dashboard or `query_health_indicators`.

The issue lists Apple's eleven. Checking every decoder table (`kernel.decoders.metrics_of`) found eleven more with the same empty column:

| Decoder | Metrics |
|---|---|
| Apple (11) | `hrvSDNN`, `walkingAsymmetryPercentage`, `walkingDoubleSupportPercentage`, `wristTemperatures`, `perfusionIndex`, `cyclingSpeeds`, `stairAscentSpeed`, `stairDescentSpeed`, `sixMinuteWalkDistance`, `recoveryes`, `uvExposures` |
| Garmin, Whoop, Oura, Open Wearables (11 more) | `recoveryScore`, `sleepPerformance`, `sleepConsistency`, `skinTemperature`, `temperatureDelta`, `heartRateMax`, `speeds`, `altitudeGain`, `altitudeChange`, `walkingRunningDuration`, `alcohol` |

### Change

`mirobody/res/catalog/metrics.tsv`: each of the 22 now declares the statistic its own `aggregation_policy` names:

| Policy | Methods | Metrics |
|---|---|---|
| `mean_min_max` | `avg,min,max` | `hrvSDNN` |
| `sum_delta` | `total` | `alcohol` (as the 12 other `sum_delta` metrics that declare one) |
| `last` | `last` | the other 20 (as 581 other series metrics) |

The catalogue is not uniform for `mean_min_max`: of the eight such series on `main`, two declare `avg,min,max` and three (`hrvRMSSD` among them) declare `avg` alone. `hrvSDNN` takes all three its policy names.

**WHOOP's `maxHeartRateProfile` stays stored and unshown.** It is the ceiling set in the profile, not a measurement: `res/crosswalks/unmappable.tsv` files it as `NOT_MEASUREMENT` ("the profile ceiling, not the day's measured maximum"). A daily row would sit beside the measured maximum (`heartRateMax`, `dailyHeartRateMax`) and be read as one. The guard exempts it by name.

None of the 22 is produced by any other path. `schema/41_device_rules.sql` only holds their ingestion range filters, and no derive rule names them, so no day gets two rows.

### Days stored before this release

They are not rebuilt on their own. The aggregator's cursor is `series_data.update_time`, and it groups by (person, indicator, day), so it revisits a day only when that indicator's points for that day are written again. Rerunning `mirobody import apple <export.zip> --into <user id>` rebuilds every day the export covers (it calls `recalculate_date_range` over the export's span) and stores no point twice. The CHANGELOG says so.

### Guard

`mirobody/tests/test_decoder_metrics_reach_a_day.py` fails when any decoder writes a series metric that declares no statistic, so the next one cannot be invisible. Sleep stages (`duration_union`) are exempt, because their nightly figures come from the derive rules (`standardize/derive/rules.py`). A second test fails when the `maxHeartRateProfile` exemption stops naming a decoder output or gains a statistic, so the exemption cannot rot into hiding a different metric. The file also pins the mapping above, and that `hrvSDNN` gets `avg`, `min` and `max` rules. Against `main`, three of the four fail (the exemption test passes there, as it should).

### Verified on PostgreSQL 17

A synthetic Apple export: six HRV (SDNN) points over three days, three walking-asymmetry points, three heart-rate points.

| Step | Code | What `th_observation` holds |
|---|---|---|
| `mirobody import apple … --into 1` | `main` | heart-rate dailies only; `series_data` has 6 `hrvSDNN` and 3 `walkingAsymmetryPercentage` points |
| schema replay, as on an upgraded server's start | this branch | unchanged |
| the same import again | this branch | `dailyAvg/Min/MaxHrvSDNN` and `dailyLastWalkingAsymmetryPercentage` for every day; `series_data` still 6 / 3 / 3 |
| `--into 2 --tz Asia/Shanghai`, fresh | this branch | HRV per local day avg / min / max: 51 / 40 / 61, 41.5 / 35 / 48, 70 / 70 / 70 (the hand-computed figures) |
| `query_health_indicators` (person 2) | this branch | the catalogue lists the four new dailies; `view="day"` returns the figures above |

### Gates

```
ruff check mirobody examples                         → all checks passed
python -m compileall -q mirobody                     → ok
pytest -q, [app,test]                                → 1351 passed, 122 skipped, 12 xfailed
pytest mirobody/tests/test_postgres_regressions.py   → 122 passed (PostgreSQL 17)
lint-imports                                         → 6 kept, 0 broken
check_comment_style                                  → 0 problems
check_versions                                       → every file names 1.5.10
maintainers' local suite, same copy on main and here → identical: 2756 passed, 272 failed,
                                                       126 errors on both (stale cases, not this change)
```

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d9ccffcb4cdc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.