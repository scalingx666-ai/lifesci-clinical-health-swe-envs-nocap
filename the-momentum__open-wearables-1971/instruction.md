# Issue

**Title:** fix(backend): store Apple sleeping wrist temperature as skin_temperature

## Description

## What does this change?

Apple Watch's overnight wrist temperature goes to `skin_temperature` instead of `body_temperature`.

## Why?

It's a skin reading (~34-35 °C), so it shouldn't share a series with thermometer readings. Other wearables already store their nightly reading as `skin_temperature`.

No data migration, on purpose. The SDK never sent this type, and older Apple Health XML imports stay in `body_temperature`. Those are rare, and wrist readings there can't be reliably told apart from thermometer ones.

Related issue:

## How did you test this?

Same SDK sync payload: thermometer 36.6 °C + wrist 34.8 °C.

| | thermometer 36.6 | wrist 34.8 |
|---|---|---|
| Before (`POST /sdk/users/{id}/sync` on a local instance with the current mapping) | `body_temperature` | `body_temperature` |
| After (same payload through `ImportService.load_data` on this branch) | `body_temperature` | `skin_temperature` |

Added `test_apple_wrist_temperature_maps_to_skin_temperature`. SDK import and provider tests pass (892) in Docker. Regenerated the coverage table, so Apple now shows `skin_temperature`.

Not tested: real Apple Watch data. My test iPhone has no wrist temperature samples, and HealthKit doesn't let apps write this type.

Should ship before or together with the iOS SDK release that includes the-momentum/open_wearables_ios_sdk#67.

## AI usage

Claude Code (Claude Opus 5.5): investigation, the change, tests and this description, reviewed by me.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Apple sleeping wrist temperature readings are now categorized as skin temperature, while standard Apple body temperature readings remain categorized separately.

* **Documentation**
  * Updated Apple’s listed support for skin temperature.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f067907b93d0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.