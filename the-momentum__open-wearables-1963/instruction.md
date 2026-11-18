# Issue

**Title:** feat(backend): store Garmin bone mass and body water percentage

## Description

Smart-scale bone mass and body water readings from Garmin were dropped on ingestion. They are now stored and available through the timeseries API. Body water comes in different units depending on the source: Garmin reports a percentage, while Withings and Health Connect report mass. Rather than converting one into the other, it gets a separate percentage series type, the same split as body fat percentage and body fat mass.

## Changes

- New `body_water_percentage` series type (percent), next to the existing `body_water_mass` (kg)
- Garmin body composition now stores bone mass (converted from grams to kg) and body water percentage
- Webhook events for `bone_mass`, `body_water_mass` and `body_water_percentage`, both as `body_composition.created` and as per-metric `series.*.created` events
- **Behavior change:** bone mass and body water mass from Withings were already stored but never sent webhooks. They will now emit events to subscribers of `body_composition.created`

_(Added during review by Sebastian Kalisz:)_ The new events fire only for providers whose samples go through the timeseries service (Withings here). Garmin's ingestion writes samples straight to the repository, so no Garmin series sends webhooks today, and the new Garmin bone mass and body water samples don't either. That gap covers every Garmin series and is left for a separate issue.

## How it was tested

- Ran the full Docker stack locally from this branch.
- Created a test user and attached a Garmin connection with a made-up Garmin user ID directly in the local database. No real Garmin account or device was involved.
- Sent a body composition push to the Garmin webhook endpoint, the same way Garmin delivers data. The payload was written by hand from the example in Garmin's Health API documentation (v1.2.3), with bone mass in grams and body water as a percentage. The request went through the normal path: webhook endpoint, background worker, database.
- Checked the stored values directly in the local database, then read them back through the public timeseries API, both raw and aggregated hourly.

## Follow-up: Android SDK

The Android SDK does not send these metrics yet:

- Health Connect `BoneMassRecord` / `BodyWaterMassRecord` are not read
- Samsung Health's `TOTAL_BODY_WATER` field is not read (Samsung has no bone mass field)

Once the SDK sends them, the backend needs the matching SDK metric type mapping. It is intentionally left out of this PR so coverage docs don't advertise Health Connect support before it exists.

## Historical data

only newly ingested Garmin body composition readings will contain `bone_mass` and `body_water_percentage`. Readings stored before this change are not reprocessed, and no backfill is planned.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

## Summary by CodeRabbit

- **New Features**
  - Added Garmin support for recording bone mass and body-water percentage measurements.
  - Added webhook events for bone mass, body water mass, and body-water percentage updates.
  - Added body-water percentage as a supported time-series metric, using average aggregation.
- **Documentation**
  - Updated metric definitions and provider coverage information to reflect supported measurements.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `815c8a42cccb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.