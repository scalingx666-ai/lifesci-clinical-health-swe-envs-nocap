# Issue

**Title:** fix(server): reschedule a Cron when its target or onBehalfOf changes

## Description

## Problem

A Cron tick unregisters the job scheduler when the Cron's `targetReference` bot or `onBehalfOf` membership no longer resolves. `addCronJobs` only upserted the scheduler when the effective cron string changed, so repointing the Cron at a replacement bot (or membership) with the same `cronString` was a no-op: the Cron stayed `active: true` but never ran again.

## Fix

`addCronJobs` now delegates to `shouldUpdateSchedule(previousVersion, resource)`, which returns true when:

- the effective cron string changes (`cronString`, `active`, `endTime`, or a Bot's `cronTiming`/`cronString`), or
- a Cron's `targetReference` or `onBehalfOf` changes.

Anything else (e.g. `parameter`) still leaves the scheduler alone. Each tick already reads the Cron fresh, so the scheduler only needs to exist for the new target to run.

## Tests

The existing "execBot unregisters the job once its target bot / onBehalfOf membership is deleted" cases now continue past the unregister: an unrelated `parameter` edit doesn't upsert, and repointing only the dead reference upserts `Cron/<id>` with the unchanged pattern. Both cases fail without the reference check.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dcf975363df0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.