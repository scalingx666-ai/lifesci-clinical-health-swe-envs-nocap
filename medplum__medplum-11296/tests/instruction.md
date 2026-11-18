# Issue

**Title:** [SchedulingWorkspace] Don't page the calendar to a day already on screen

## Description

After booking, blocking, or "book now", the workspace pages the calendar to the new event's day. The 4 Day view starts at whatever date it is paged to, so it shifted even when that day was already visible. gotoDate now stays put when the date is inside the visible range.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c6c86f9e1f93`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.