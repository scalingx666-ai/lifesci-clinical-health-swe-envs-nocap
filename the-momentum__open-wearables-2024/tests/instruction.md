# Issue

**Title:** fix(backend): day reads take samples for days the rollup hasn't caught up with

## Description

## What does this change?

With the rollup on and caught up, `1day` / `1week` / `1month` reads used stored day rows only, so a day changed since the last run read stale and a day with no row yet didn't appear. Now:

- A read asks the rollup queue which of its sources' days are still waiting (queued or in progress) and counts only those days from samples. Our row is replaced, a provider's own row stays, and days retention emptied keep their rows.
- The queue keeps a small per-source index of waiting days, so the check is one Redis round trip whatever the queue size or range, open-ended ranges included. It runs on a worker thread alongside the read's first DB query; if Redis is slow (> 50 ms) or down, the read falls back to stored rows and logs it.
- `source_selection=reconcile`: a stored merged day whose samples changed since is merged again instead of served stale.

Also fixes `per_range` day reads (on main since #1934): winner selection only looked at day rows, so with the rollup off (the default) `1day` + `per_range` returned nothing for sources without provider day values. It now also looks at samples wherever the read counts from them.

## Why?

The alternative was always filling missing days from samples, as when the rollup is off, which gives up what the rollup buys: day reads 2–9x faster (44–96 ms vs 822–829 ms for a year). Checking the queue limits sample reads to the days actually behind, usually today and maybe yesterday.

Breaking change: none in the API. `1day` + `per_range` with the rollup off now returns data where it returned nothing before.

_(Added during review by Sebastian Kalisz:)_ The same queue check also applies to `/summaries/activity` and `/summaries/body`: a day still waiting for the rollup is counted from its samples there too, so today's steps or heart rate in a summary follow the newest samples instead of the last stored row.

## Changes during review

> _Added during review by Sebastian Kalisz._

- A waiting day keeps our row for a series that has no samples that day (e.g. an archived day), as the rollup does. Before, the read dropped it until the next run.
- `reconcile`: a stored merged day is merged again only when a source of that series and day is waiting. Before, a source of another series (e.g. a scale sending weight) made every stored merge of that day count as stale.
- `per_range` on day reads probes waiting samples by local day, like the read itself. Before, a sample just past the range's last local day (by its offset) could crown a source that then returned nothing.
- A slow or failing Redis is logged as a warning, not sent to Sentry on every read.
- Dropping the queue (rollup off) reads the queued sources and deletes their keys in one Lua script, so a write in between leaves no orphaned per-source index.
- The stack now includes current `main` (with #2026), so this path runs once the history rollup is enabled. Tests raise the queue timeout so they check the logic, not Redis latency, and cover the summaries.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Period-based time-series results now include recent sample data while daily rollups are pending, including days without an existing aggregate.
  * Updated samples are reflected in results even after a day was previously reconciled. Provider-computed data remains available, and samples removed by retention are excluded.
  * Source selection and ranking now account for available samples as well as daily aggregates, including when rollup history is incomplete.
  * Activity summaries now include newly added samples for days whose rollups have not yet caught up.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `65b7de85c2ea`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.