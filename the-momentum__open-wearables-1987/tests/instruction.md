# Issue

**Title:** fix(backend): map SDK cycling power, cadence and speed to workout details

## Description

## What does this change?

Workout stats the iOS and Android SDKs already send now land in workout details: iOS 17+ `averageCyclingPower`/`averageCyclingCadence`/`averageCyclingSpeed` and Samsung `meanPower`/`maxPower`/`meanRpm`. They were silently dropped before. Also drops `moving_time_seconds` from the Apple and Health Connect [coverage matrix](https://docs.openwearables.io/providers/coverage), since no SDK stat sets it.

## Why?

Cycling workouts from iOS and Samsung lost power, cadence and speed even though the target fields already existed.

When several stats target the same field, the value no longer depends on payload order. Cycling power wins over `averageRunningPower` (Health Connect sends power for any workout under that key), and the workout-level `averageSpeed` wins over sensor averages, which keeps the current iOS behaviour.

Google Health was reusing the Apple field set but does set `moving_time_seconds` itself, so it now declares exactly the fields it fills.

Left out on purpose until we decide whether to store them: Samsung `count`, `meanCalorieBurnRate`, `maxCalorieBurnRate`, `inclineDistance`, `declineDistance`, `maxRpm`.

## How did you test this?

Ran the same workout stats through the import service in Docker on `main` and on this branch:

```
iOS cycling (averageRunningPower 240, averageCyclingPower 182.4, averageCyclingCadence 87.6, averageCyclingSpeed 7.85)
Before: average_watts 240.0, average_cadence None, average_speed None
After:  average_watts 182.4, average_cadence 87.6, average_speed 7.85

Samsung session (meanSpeed 7.19, maxSpeed 14.2, meanPower 171.5, maxPower 612, meanRpm 84, maxRpm 118)
Before: average_watts None, max_watts None, average_cadence None, average_speed 7.19, max_speed 14.2
After:  average_watts 171.5, max_watts 612.0, average_cadence 84.0, average_speed 7.19, max_speed 14.2
```

Not tested with a real device sync; the payloads follow what the SDKs build (`Types.swift` on iOS, `SamsungHealthManager.kt` on Android).

## AI usage

Claude Code (Opus 5.5) for the implementation, tests and the PR draft.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Added support for importing cycling power, cadence, and speed statistics from Apple and Samsung workout data.
  * Workout details now prioritize the most relevant statistic when multiple sources provide a value, regardless of input order.
  * Added Samsung workout coverage for cadence and power metrics.

* **Bug Fixes**
  * Preserved moving-time values during import instead of converting them to integers.

* **Documentation**
  * Updated the provider coverage guide and API documentation to reflect supported workout statistics and provider coverage.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1d7be397c430`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.