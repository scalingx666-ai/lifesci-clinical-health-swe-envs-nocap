# Issue

**Title:** fix: Include workout-only days in daily summary

## Description

`/summaries/activity` builds its list of days from time-series data (`data_point_series`). Workouts only fill in days that already exist there, so a day with only a workout is never returned.

Something like this could happen e.g. with Strava without ingesting workout samples (which iirc approx. 10% of known instances have it set to `True`)

Credit to @andreaf08-bit, who in #1377 included a fix, but it wont work anymore and merge conflicts appeared in the meantime.

The change here:
Days with only workouts return metrics such as:
-  date, source
- elevation meters
- floors climbed

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Activity summaries now include dates with workouts even when no other activity data is available. These entries identify the workout provider, while unavailable metrics remain blank.
* **Bug Fixes**
  * Workout details are matched to summaries by provider, helping keep data from different providers separate. When providers report competing activity data, summary metrics follow the selected provider’s priority.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `619d5d77f1ed`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.