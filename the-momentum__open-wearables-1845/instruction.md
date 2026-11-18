# Issue

**Title:** fix(backend): page sleep summaries by night, not by source row

## Description

## What does this change?

`/summaries/sleep` now pages by night, so a page holds `limit` nights and `has_more` is right when more than one source recorded the same nights.

## Why?

Details are in #1831. `get_sleep_summaries` applies the cursor and `limit + 1` to the per-(date, source) rows, then `_filter_by_priority` keeps one source per night, and only after that does the service check `has_more`. With two sources a page comes back short with `has_more: false`, and a night can get split across pages and summarised from the lower priority source.

The repository now picks the next `limit + 1` sleep dates past the cursor first, using the same local date and filters as the aggregate, and then aggregates every source's rows for those dates. So the limit counts nights and a night never gets split. The aggregate is filtered on the range of those dates instead of `IN` the list, which selects the same nights since they're consecutive among the nights with sleep, but Postgres plans it a lot better (more on that below). The cursor format doesn't change and old cursors still work.

It also fixes a small thing on backward pages. Main's prev query compared `(date, record id)`, so a losing source's row on the cursor's own night could leak into the previous page.

This is the same fix as #1844 for recovery. Both touch the import block of `tests/services/test_summaries_service.py`, so whichever goes in second will need a one line rebase there.

## How did you test this?

Ran the API locally against Postgres 18 and paged `GET /api/v1/users/{id}/summaries/sleep` with an API key, following `next_cursor` to the end. One user with Garmin (watch) and Oura (ring) sleep on Jan 2 to 6, default priorities, so Garmin wins:

```
           main                       this branch
limit=1    Jan 2, has_more=false      Jan 2 to 6, one per page, all garmin
limit=2    Jan 2-3, has_more=false    Jan 2-3, 4-5, 6, all garmin
limit=50   Jan 2 to 6, garmin         Jan 2 to 6, garmin
```

New service tests page forward with limit 1 and 2 and check the previous cursor with two sources per night, and a new API test checks that paging with limit 2 returns the same nights as one big page. All 4 fail on main. The full backend suite passes (3108 passed, 3 skipped), ruff is clean, ty shows the same 7 otel import errors as main, and the OpenAPI check is clean.

Timing, with 20 users who each have Garmin and Oura sleep every night for a year, default page of 50:

```
main                          54 ms, 26 nights, has_more=false
date list with IN             431 ms, 50 nights
date range (this PR)          65 ms, 50 nights
```

The `IN` version made Postgres compare every sleep record against each page date in a nested loop, because it has no estimate for the computed local date. Paging through the whole year with the range version returns all 365 nights once.

Backward pages still come back newest first, and following `previous_cursor` twice repeats a night. That's the same on main and in recovery, so I left it for a separate fix.

## AI usage

Claude Code (Claude Opus) helped trace the bug, write the fix and tests, and draft this description. I reviewed the change and ran the checks above.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Bug Fixes**
  * Sleep summaries now show only the highest-priority source for each night when multiple sources report the same sleep.
  * Forward and backward pagination return nights in date order, with the preferred source selected consistently across pages.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `72512d0d7782`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.