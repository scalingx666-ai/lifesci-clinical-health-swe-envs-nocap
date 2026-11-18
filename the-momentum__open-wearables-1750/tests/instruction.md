# Issue

**Title:** feat(backend): ingest HRV RMSSD from HealthKit (iOS 27+)

## Description

## What does this change?

Apple SDK records of type `HKQuantityTypeIdentifierHeartRateVariabilityRMSSD` (new in iOS 27) are now stored in the existing `heart_rate_variability_rmssd` series instead of being dropped.

## Why?

iOS 27 HealthKit reports HRV as RMSSD next to SDNN. The iOS SDK starts sending it in the-momentum/open_wearables_ios_sdk#70, but the backend has no mapping for the identifier, so `get_series_type_from_metric_type` returns `None` and the sample is silently skipped.

I reused the existing series rather than adding an Apple-specific one: Health Connect, Oura, Whoop, Garmin and others already write RMSSD there, so Apple RMSSD becomes directly comparable and no migration is needed. SDNN stays in its own series - the two are different measures and must not be merged.

## How did you test this?

Same Apple payload (one SDNN and one RMSSD record, `unit: "ms"`) through `ImportService._build_statistic_bundles`:

```
main:   [('heart_rate_variability_sdnn', '48.2')]
branch: [('heart_rate_variability_sdnn', '48.2'), ('heart_rate_variability_rmssd', '36.7')]
```

That case is now a test in `tests/integrations/test_sdk_import.py`. Full backend suite passes, and `export_openapi.py --check` passes after regenerating `openapi.json` and `providers/coverage.mdx`.

Not tested: a real sync from an iOS 27 device - I don't have real RMSSD samples from a watch yet, only the iOS 27 simulator for the SDK side. The unit (`ms`) comes from the HealthKit header and the SDK change, not from an observed payload.

## AI usage

Claude Code (Claude Opus 5.5): found the new identifier in the iOS 27 SDK headers, drafted the mapping, test and docs changes, and this description. I reviewed the changes.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

- **New Features**
  - Apple HealthKit data now supports importing HRV RMSSD measurements separately from SDNN, with millisecond values preserved. RMSSD is available on iOS 27 and later.
- **Documentation**
  - Updated the supported health data types and provider coverage information to include Apple HRV RMSSD.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `17262c1b43e1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.