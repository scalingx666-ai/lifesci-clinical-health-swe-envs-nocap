# Issue

**Title:** fix(integrations): fetch Polar sleep nights that become available late

## Description

Takes over #1818 by @slavarosin

## What does this change?

Polar sleep sync now also fetches nights that show up in `/v3/users/sleep/available` after their date has left the sync window, unless they are already stored (matched by their `sleep-<date>` external id). ~~On top of the original commit, the Polar sleep id is built by one helper instead of in three places.~~ _(Added during review by Sebastian Kalisz:)_ the last commit went back to building the id inline, so the code builds it as on main.

## Why?

A night appears in `/sleep/available` only after the watch syncs with Polar Flow. For someone who syncs every few days that is long after the window passed, and the sync fetched only available nights inside the window, so those nights were never stored in pull mode. Webhook mode already gets them through the SLEEP event.

> _Added during review by Sebastian Kalisz._
>
> - Each late night costs one extra AccessLink call, once: after it is stored under `sleep-<date>`, later syncs skip it. AccessLink lists nights for 28 days, so at most 27 such calls per user per sync, and in steady state only the nights that arrived since the last sync.
> - Re-fetching is idempotent: a stored night is skipped, and a new late night goes through `create_or_merge_sleep` like any other, so `sleep.created` goes out once for it.
> - A late night is also skipped when a stored Polar sleep overlaps its `start_time`–`end_time` from `/sleep/available`. This covers a night merged into the next one (#2012), whose record carries only the later date's id: without the check it would be re-fetched on every sync for 28 days, adding its time in bed each time. Nights inside the sync window are still re-fetched every sync, as on main.

## How did you test this?

- @slavarosin tests: a late night outside the window is fetched, a stored late night is not fetched again, another user's night doesn't count as stored.
- Full backend suite

## AI usage

Claude Code helped review the changes and write the follow-up refactor.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Sleep records Polar reports after their date falls outside the sync window are now retrieved when available. Records already stored for the same user are skipped, including nights covered by an overlapping stored sleep record. Records belonging to other users do not prevent retrieval.
* **Documentation**
  * Clarified that sleep records may become available days after a device syncs with Polar Flow and can remain available from Polar for up to 28 days.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7ca121dd4e48`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.