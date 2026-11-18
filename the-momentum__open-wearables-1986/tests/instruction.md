# Issue

**Title:** feat(backend): gate Apple percentage scaling on iOS SDK version

## Description

## What does this change?

Apple body fat and walking percentages are multiplied by 100 only when the iOS SDK version is below 0.17.0. From 0.17.0 the SDK sends them on a 0-100 scale itself (the-momentum/open_wearables_ios_sdk#77).

```jsonc
// iOS SDK 0.16.0 and older (unchanged): x100, stored as 30.4
{"provider": "apple", "sdkVersion": "0.16.0", "data": {"records": [
  {"type": "HKQuantityTypeIdentifierBodyFatPercentage", "value": 0.304, "unit": "%"}
]}}

// iOS SDK 0.17.0+: stored as sent, 30.4
{"provider": "apple", "sdkVersion": "0.17.0", "data": {"records": [
  {"type": "HKQuantityTypeIdentifierBodyFatPercentage", "value": 30.4, "unit": "%"}
]}}
```

The same applies to `HKQuantityTypeIdentifierWalkingAsymmetryPercentage`, `HKQuantityTypeIdentifierWalkingDoubleSupportPercentage` and `HKQuantityTypeIdentifierAppleWalkingSteadiness`.

**Release order:** this ships in Open Wearables 0.11.0. Anyone who upgrades the iOS SDK to 0.17.0 while still on Open Wearables 0.10.0 or older gets body fat and walking percentages multiplied twice (body fat `30.4` stored as `3040`), and a later backend upgrade doesn't fix rows already stored. The iOS SDK changelog states the 0.11.0 requirement in a warning block (the-momentum/open_wearables_ios_sdk#77).

## Why?

The iOS SDK sends `HKUnit.percent()` values as a 0-1 fraction labelled `"%"`, while Android sends 0-100, so the backend had to special-case Apple. The SDK now scales them, as it already does for SpO2. Apps built with older SDK versions will keep sending fractions for a long time, so the x100 stays for them.

A missing or unparseable `sdkVersion` keeps the x100. Getting it wrong the other way (3040 instead of 30.4) would be worse than today. Pre-releases of 0.17.0 count as new.

The Apple XML import doesn't go through this conversion and is unchanged.

Related issue: #1648

## How did you test this?

Local stack on this branch, Flutter example app on an iPhone (iOS 27.0.1), body fat sample added by hand in Apple Health, then checked `data_point_series`:

| App build | `sdkVersion` sent | Entered in Health | Stored |
|---|---|---|---|
| SDK from this PR | `0.17.0` | 50% | `50.000` |
| Released SDK 0.16.0 | `0.16.0` | 51% | `51.000` |

SDK side: the-momentum/open_wearables_ios_sdk#77.

## AI usage

Claude Code (Claude Opus) for the implementation and the PR description.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Corrected percentage values for body-fat and walking metrics imported from older Apple SDK versions, so they’re displayed at the expected scale.
  * Percentage values from newer Apple SDK versions and non-Apple providers remain unchanged.
* **Documentation**
  * Added guidance to check SDK and backend version compatibility and upgrade the backend before adopting a newer SDK. Data already stored incorrectly may require separate correction.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5e809da32e3f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.