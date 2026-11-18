# Issue

**Title:** fix(backend): count sleep interruptions in the daily sleep summary

## Description

## What does this change?

`interruptions_count` in `GET /summaries/sleep` is now filled in: awakenings longer than 5 minutes inside the main sleep, counted from each session's stage timeline. Naps are left out. It stays `null` when the day has no main sleep or the timeline of one of its main sessions has no sleep stage (sleeping, light, deep or rem), no timeline at all included.

The summary and the sleep score now count awakenings with the same functions, `awakenings()` and `significant_awakenings()` in `app/algorithms/sleep.py`, and the same threshold (`sleep_config.significant_wake_threshold_mins`):
- Awake blocks that directly follow each other count as one awakening. Apple sometimes records a single wake-up as several back-to-back awake blocks; counted block by block, one wake-up could turn into several awakenings, and a wake-up longer than 5 minutes split into shorter blocks would not count at all.
- Where blocks overlap, as two merged sessions can leave them, the earlier block keeps the overlap, as the merge does when it totals the stage minutes; `in_bed` and `unknown` blocks take no part, as in the SDK's stage clean-up. Overlapping awake blocks count as one awakening with the overlap counted once, and a block that an earlier one covers whole is dropped.
- The sleep period starts at the first and ends at the last sleeping/light/deep/rem block left after that, so an `in_bed` or `unknown` block (Polar with no skin contact, Google RESTLESS) at the edges doesn't turn lying awake into an interruption.
- A timeline with no such block gives `null` in the summary, and the score falls back to the reported awake minutes, as for a night without a timeline.
- Stages are ordered by time first. Gaps in the timeline are not treated as time awake.

This changes the sleep score's interruptions pillar for nights with back-to-back or overlapping awake blocks, `in_bed`/`unknown` blocks at the edges, an unsorted timeline or a timeline with no sleep stage. Stored scores are not recomputed.

Sleep summaries now load sessions only for the nights on the page instead of the whole requested range, and stage timelines only for the page's main sleeps (one source per night, no naps).

## Why?

The field was always `null`, and the summary and the score should agree on what an interruption is.

Related issue: #1659

## How did you test this?

- Unit tests for `awakenings()`: falling asleep and final wake-up, back-to-back awake blocks, gaps, `in_bed`/`unknown` edges, unsorted timeline, overlapping awake blocks, an `in_bed` or `unknown` block spanning the night, a sleep stage inside an earlier awake block and a timeline with no sleep stage. Score tests for the new rule and the awake-minutes fallback; summary tests for the threshold, naps, several main sessions, missing timelines and timelines with no sleep stage; tests that only the page's nights are loaded and only its main sleeps' stage timelines are read. Full backend suite passes
- Ran the API locally on seed data and compared every returned `interruptions_count` with an independent count straight from the database: all matched

Known limits:
- The WHOOP API returns stage totals only, no timeline, so WHOOP nights are `null`
- The sleep score moves out of this repository on November 6; the health-scores extension needs the same awakening rule (separate PR there)

## AI usage

Claude Code was used to propose the fix, implement the tests and review the changes.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

## Summary by CodeRabbit

* **New Features**
  * Sleep summaries now include an interruption count for awakenings longer than five minutes during main sleep. Naps are excluded, and the count is unavailable when there is no main sleep or required sleep-stage data is missing.

* **Bug Fixes**
  * Sleep interruption scoring now combines adjacent awake periods and excludes time before sleep begins or after the final wake.
  * Sleep summaries now include session details for the nights shown on the current page.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a6732845951`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.