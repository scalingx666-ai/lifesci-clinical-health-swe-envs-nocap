# Issue

**Title:** fix: derive Polar sleep efficiency and drop repeated hypnogram intervals

## Description

## What does this change?

- Polar sleep gets `sleep_efficiency_score`: Polar Flow's actual sleep share, the night minus its interruptions over the night. A night without reported interruptions, or with interruptions that don't fit it, gets none. Polar's API reports no efficiency, so it was always empty.
- Polar's `sleep_total_duration_minutes` also counts sleep Polar couldn't assign a stage to (`unrecognized_sleep_stage`).
- A data migration, `backfill_polar_sleep_efficiency`, sets the efficiency on stored Polar nights from their stored minutes awake. It waits for `dedupe_polar_sleep`, since a night re-synced before #1870 may hold its minutes more than once until that has run. Nights still in Polar's 90-day window also get it on their next re-sync.
- The hypnogram drops repeated stage intervals, compared as instants, and keys a span by its start and end, so a night whose stages were stored twice can be expanded again. The deduplication comes from #1914 by @malicaeus.

## Why?

#1908: Polar nights showed no efficiency, and a night whose stages were stored twice couldn't be expanded. The doubled time in bed reported there was fixed by #1870.

## How did you test this?

- Polar tests: efficiency from the interruptions, with or without stages, kept to two decimals; none without interruptions or when they don't fit the night; unrecognized sleep counted as sleep.
- Migration tests: only Polar nights change; a reported efficiency, a night without stages and one with more sleep than its window are left alone; a second run and the dry run change nothing; it waits for the Polar sleep dedupe.
- Frontend specs: repeated intervals, and an interval written with another offset, are drawn once.
- Full backend suite, `ruff`, `ty`, frontend unit tests, `prettier` and `eslint` pass.

## Breaking change

_(Added during review by Sebastian Kalisz:)_ Polar's `sleep_total_duration_minutes` grows by the night's unrecognized sleep, for new nights and for nights still in Polar's 90-day window on their next re-sync. Older nights keep the value without it: the unrecognized seconds weren't stored, so they can't be backfilled. Polar nights start when the user falls asleep, not when they go to bed, so their efficiency runs higher than that of providers that count time in bed.

## AI usage

Claude Code for tracing the issue and first drafts of the fix, the migration and the tests.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Polar sleep records now include sleep-efficiency scores based on time asleep versus time in bed, with eligible existing records updated.
  * Unrecognized sleep stages count toward total sleep duration. Polar sleep-efficiency support is also reflected in provider documentation.

* **Bug Fixes**
  * Sleep-stage charts no longer duplicate identical intervals, including intervals with timestamps in different UTC offsets.
  * Chart spans that share a start time but have different end times now render separately.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `75b0957701cf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.