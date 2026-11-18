# Issue

**Title:** fix(backend): stop storing the relaying iPhone as the model of third-party HealthKit sources

## Description

## What does this change?

When another app writes to Apple Health (Oura, Zepp Life, a BLE strap via `com.apple.BTLEServer`), the iOS SDK reports the iPhone it ran on (`iPhone16,1`) as the device model. We stored that as the source's model and inferred `phone` from it, so an Oura ring synced through Apple Health showed up as a phone and lost to real phones in [device type priorities](https://docs.openwearables.io/developer-portal/settings/priorities).

Now the iPhone code is dropped for third-party writers, at ingest and in stored rows, and the type is re-inferred without it. Only a few writer names map to a type today (`SOURCE_NAME_KEYWORDS`: Oura → `ring`, AutoSleep → `watch`, Mi Band/Xiaomi → `band`; Whoop → `band` via model keywords), so most writers (Zepp Life, Strava, Garmin Connect, ...) end up with no type instead of `phone`.

## Why?

the-momentum/open_wearables_ios_sdk#73 makes the SDK send the writer's own `HKDevice.model` instead, or `null` (Oura attaches no device). #1781 already prepared for that, but two cases broke with it:

1. **Source split.** Rows stored before 0.10.0 (#1781) have no `source_app_id` until the writer syncs again. If that next sync comes from the fixed SDK (`deviceModel: null`), it doesn't match the old `iPhone16,1` row and a second source is created. The old history stays on the first one.
2. **Model comes back.** After clearing the model, the next sync from an older SDK fills `iPhone16,1` in again, because a row without a model takes whatever arrives.

So the backend now drops the iPhone code for third-party writers itself, which also makes older SDKs send the same thing as the fixed one. The `phone`/`watch` type the older SDKs derive from that code is dropped with it, otherwise a writer without a known name (Garmin Connect, Zepp Life) would still be stored as `phone`. No gating on the SDK version is needed. A legacy row is matched by writer name when the incoming record has no iPhone model. Rows already stamped with an app id get cleaned up by a one-off migration (`clear_relayed_host_models.py`, runs once per instance from `app.sh`). Legacy rows without an app id can't be told apart from the iPhone's own data in SQL, so they are fixed on the writer's next sync instead.

Trade-off: a third-party app running on the Watch (e.g. WorkOutDoors) or a strap relayed by the Watch also loses its `Watch…` code and the `watch` type. This follows `is_host_model` from #1781; I changed the `com.apple.BTLEServer` expectation in `test_device_types.py` accordingly. Worth a second look.

## Release order

Release this before the-momentum/open_wearables_ios_sdk#73. This change works with every SDK version, since older ones get the iPhone code dropped at ingest. The fixed SDK on 0.10.0 or 0.11.0 without this change still splits sources stored before 0.10.0 (case 1 above), and never clears the iPhone model from the others.

Related issue: the-momentum/open_wearables_ios_sdk#71

## How did you test this?

I ran the same iOS SDK payloads (one Oura heart rate record per sync) through `import_service.load_data` against a throwaway Postgres, once with `main` and once with this branch. Below is `data_source` for the user after each step. Step 0 is a row as 0.9.0 stores it.

**First sync after the upgrade comes from the fixed SDK**

| step | `main` | this branch |
|---|---|---|
| 0. stored by 0.9.0 | `iPhone16,1` · app_id – · `phone` | `iPhone16,1` · app_id – · `phone` |
| 1. fixed SDK (`deviceModel: null`) | `iPhone16,1` · app_id – · `phone` (old history)<br>`NULL` · `com.ouraring.oura` · `ring` (new) | `NULL` · `com.ouraring.oura` · `ring` |
| 2. old SDK (`deviceModel: iPhone16,1`) | `iPhone16,1` · app_id – · `phone` (old history)<br>`iPhone16,1` · `com.ouraring.oura` · `ring` | `NULL` · `com.ouraring.oura` · `ring` |

**Old SDK first, then fixed SDK**

| step | `main` | this branch |
|---|---|---|
| 1. old SDK | `iPhone16,1` · `com.ouraring.oura` · `phone` | `NULL` · `com.ouraring.oura` · `ring` |
| 2. fixed SDK | `iPhone16,1` · `com.ouraring.oura` · `phone` | `NULL` · `com.ouraring.oura` · `ring` |

All samples land on the single source in each branch run.

**Migration** on a row as `main` stores it after an old SDK sync, next to an Apple Watch source:

```
com.ouraring.oura: iPhone16,1 (phone) -> NULL (ring)
Cleared the relaying host model on 1 data source(s)
    model=Watch7,5  source=Apple Watch  app_id=com.apple.health.A1B2  type=watch
    model=None      source=Oura         app_id=com.ouraring.oura      type=ring
```

The source objects the fixed SDK produces on a real iPhone (Polar H10, Withings, Fitbit Air, Garmin, ...) are in the-momentum/open_wearables_ios_sdk#73. Their models resolve here to `chest_strap`, `scale` and `band`.

Not tested: a real device sync end to end, and a dry run of the migration against our test instance.

## AI usage

Claude Code (Claude Opus 5.5): traced the data source matching from #1781, wrote the change and the migration, and ran the before/after scenario above.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Improved device details for data relayed through an Apple phone: the phone’s model is no longer shown as the connected device’s model, and the device type is retained when available.
  * Existing affected records are updated automatically during startup. Apple-produced device entries and records from other providers remain unchanged.
  * When a relayed device stops reporting a model, its previous phone model is cleared rather than retained. Legacy records can be matched to the correct data source without merging a separate phone entry.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8adb8d0b2fff`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.