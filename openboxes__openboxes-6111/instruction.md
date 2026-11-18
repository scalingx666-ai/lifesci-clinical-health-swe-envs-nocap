# Issue

**Title:** OBLS-837 Report order level pick progress on pick task search

## Description

**Link to GitHub issue or Jira ticket:** https://openboxes.atlassian.net/browse/OBLS-837

**Description:**
The pick task search is status filtered, so a caller asking for the open queue (`status=PENDING&status=PICKING`) never receives the lines of an order that are already picked. A partially picked order is therefore indistinguishable from an untouched one: it reports fewer lines than it has and no sign that anybody started it.

**Changes**
- Each task now carries the progress of the order it belongs to: `orderTotalTaskCount`, `orderOpenTaskCount` and `orderPickStatusCode`.
- The fields are transient and populated by `PickTaskService.search` from a single projection query over the requisitions in the page, so there is no schema change. The completed rows are already in the `pick_task` view while the requisition sits in `PICKING`.
- Adds a `PickStatusCode` enum for the `NOT_PICKED` / `PARTIALLY_PICKED` / `PICKED` vocabulary, which until now existed only as duplicated string literals in `PickPageItem.getStatusCode` and `ReplenishmentPickPageItem.getStatusCode`. Both now return `PickStatusCode.X.name()`, so the existing responses are unchanged.
- A `STAGED` line with nothing picked is the terminal marker for a zero quantity short pick with a reason code, so it is excluded from both counts and does not count as progress.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `798b9a24162e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.