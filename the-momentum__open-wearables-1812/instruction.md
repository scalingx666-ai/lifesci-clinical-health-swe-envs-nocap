# Issue

**Title:** fix(backend): make seeded users show up in recent date ranges with steps and distance

## Description

## What does this change?

Three fixes to the [seed data generator](https://openwearables.io/docs/developer-portal/settings/seed-data-generator) for things that made seeded users look broken in the dashboard:

- Data was anchored to a hardcoded 2025-01-01, so with the default 1M/3M ranges the Data Summary was empty and users showed "Synced 2 years ago". The anchor is now today's midnight UTC.
- Workouts never got a `distance`, although every seeded provider reports one. Pace-based sports now get one, derived from a per-sport speed. Garmin's `average_speed` uses the same value so the two agree.
- Some days in the activity summary had no steps. The summary takes one source per day by [provider priority](https://openwearables.io/docs/developer-portal/settings/priorities), and the seed spread steps, energy and HR across different providers and devices. Workout samples also used `source="garmin"` while continuous series used `"Garmin Connect"`, so a single device ended up as two data sources. The daily activity series now come from one device of the user's top-priority provider, workouts from that provider are recorded on the same device, and `source` is the provider name for both, as in real ingestion.

## Why?

Seeded users are what we use for demos and dashboard work, and in their current state they look like bugs.

The anchor was fixed so that a seed reproduces exactly. With today's date as the anchor, the same seed still gives the same values, just shifted to end around the day you run it. I also thought about picking providers per metric in the activity summary, so steps could come from Polar when Garmin has none. That would also help real users, but it's a product change and doesn't belong in a seed fix.

## How did you test this?

Generated users from several presets on this branch and went through them in the dashboard: Data Summary has data with the default ranges, running/cycling/swimming workouts show a distance, and every day in Activity has steps.

Before the fix, one `active_athlete` user (Garmin + Polar) had its steps only on Polar Vantage V2, while the Garmin Epix row with only active energy won every day by priority, so the summary showed 0 steps.

## AI usage

Claude Code (Claude Opus) helped me diagnose the causes of the issues I ran into while generating seed data, then implemented the fixes and double-checked them against the local DB.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Improvements**
  * Generated workout distances and speeds now reflect the sport, with running workouts receiving a distance and non-pace sports such as boxing not receiving one.
  * Daily activity summaries now include steps and are associated with the primary provider’s device.

* **Documentation**
  * Clarified that generated dates are anchored to the current day at midnight UTC; explicit date ranges still take precedence.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `58dc419a4f5c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.