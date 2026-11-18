# Issue

**Title:** Restore slack notifications on failed builds

## Description

I noticed a while ago that our internal slack notification hasn't reported build failures in a long time. This was because of my previous PR #920 where I had changed the logic to not run if there was no slack webhook url configured (so that it wouldn't fail 100% of the time on forks). But removing the `always()` meant that if a previous step failed, it wouldn't run the slack notification step.

The correct logic should be to combine both the `always()` check and the slack webhook url check

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d9094e98e4cb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.