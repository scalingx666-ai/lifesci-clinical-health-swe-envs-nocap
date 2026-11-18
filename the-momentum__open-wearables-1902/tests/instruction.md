# Issue

**Title:** fix: Remove incorrect host model device type mapping from SDK payloads

## Description

Third-party HealthKit writers (like Oura or Google Health) no longer get their device type from the "host" device the data passed through (e.g. iPhone acting as the device model when it is just middleware). The device type now can be inferred from the app's name, or is left empty when the name doesn't perfectly map onto one specific device type.

This is also related to the-momentum/open_wearables_ios_sdk#71 - though the fixes there wouldn't help, and I'm starting to get a bit skeptical about its implementation.

Apps that don't identify a device type (like Strava) go from `phone` type to `none`. That also includes existing rows

Providers that this would affect (and correctly show device type now):
- Oura (ring)
- RingConn (ring)
- WHOOP (band)
- Xiaomi / Mi Band (band)
- Amazfit Band (band)
- Suunto (watch)
- AutoSleep (watch)
- HeartWatch, or any name containing "watch" (watch)

Tested this by replaying SDK payloads from my local s3, the data sources merged succesfully.

| App id | Source name | Model | Before (derived from main's logic, not replayed) | After |
|---|---|---|---|---|
| `com.ouraring.oura` | Oura | `iPhone16,1`, `iPhone17,1` | phone | **ring** |
| `com.fitbit.FitbitMobile` | Google Health | `iPhone12,1` | phone | none |
| `com.garmin.connect.mobile` | Connect | `iPhone15,2` | phone | none |
| `com.healthdatafill.app.healthFill` | Health Fill | `iPhone12,1` | phone | none |
| `com.huaye.Drinking` | Water Tracker | `iPhone15,2` | phone | none |
| `com.apple.Health` (manual entries) | Health | `iPhone13,2` | phone | none |
| `com.apple.BTLEServer` (BLE sensor) | Bluetooth Device | `Watch7,9` | watch | none |
| `com.apple.health.*` (8 sources) | e.g. "…'s Apple Watch" | `Watch7,5`, `iPhone18,1`… | watch / phone | unchanged |

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

- **Bug Fixes**
  - Improved device-type detection for data sources that relay Apple device information through third-party apps.
  - Prevented reported iPhone or Apple Watch details from incorrectly influencing classification when the source identifies another device type.
  - Updated data-source processing and backfills to consistently use the host/source identity for classification.
  - Existing host-based records are now reclassified more accurately, including wearable sources such as rings.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d18304f8076a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.