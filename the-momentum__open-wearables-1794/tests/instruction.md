# Issue

**Title:** docs: note filled activity metrics

## Description

> _Added during review by Sebastian Kalisz._

**What this PR finally contains:** a note in the API docs (the activity summary card in `integration-guide.mdx` and the `/summaries/activity` description) that each day reports its highest-priority source and fills the metrics that source lacks from lower-priority ones, so `source` may not be the origin of every metric. The fill logic itself shipped in #2020, with active, basal and total energy taken together from one source and heart rate as one group, so the code and tests from this PR were dropped when merging `main`. The original description is kept below, struck through.

---

~~What does this change?~~

~~For the activity summary, `_filter_by_priority` still picks the highest-priority source per day as the row, but now fills each metric that row lacks from the next source that reports it. The other summaries (sleep and recovery) still pick a single source as before.~~

~~Why?~~

~~When a day's activity is split across complementary sources (steps on the phone, heart rate on the watch), electing one source dropped whatever only the other one reported. Depending on which source won, the day showed steps without HR or HR without steps.~~

~~Values are copied from one source, never summed, so a metric both sources report still comes only from the higher-priority one and cross-provider de-duplication is unchanged. `hr_avg`/`hr_max`/`hr_min` are filled as one group so a day never mixes HR stats from two devices. Activity/intensity minutes that are looked up by the winning source's key are not filled; I kept the change to the aggregate row.~~

~~Related issue: #1749~~

~~How did you test this?~~

- ~~Added three tests to `TestFilterByPriority`: complementary metrics are merged (steps from one source, HR group from the other), a metric both sources report is not summed, and without `fill_missing` the old single-source behaviour is unchanged. `backend-test` passes on CI in my fork (Postgres).~~
- ~~Ran the real `_filter_by_priority` with stubbed priority repositories against the issue's case (phone with steps, watch with HR) on both versions: before the change HR is dropped, after it the row has steps 8000 and HR 72/140/55.~~
- ~~Not tested: the endpoint against real Health Connect data.~~

~~AI usage~~

~~Claude Code helped trace the bug and draft the fix and tests; I reviewed and tested them.~~

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Bug Fixes**
  * Activity summaries now fill metric groups that are entirely missing from the highest-priority source with values from another source for the same day. Existing values are preserved and are not combined with lower-priority values.
  * Active, sedentary, and intensity minutes continue to come only from the highest-priority source. Summaries outside activity are unchanged.
* **Documentation**
  * Clarified that an activity summary’s reported source may not identify the origin of every metric, since some missing metrics can come from lower-priority sources.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6101cbf66f89`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.