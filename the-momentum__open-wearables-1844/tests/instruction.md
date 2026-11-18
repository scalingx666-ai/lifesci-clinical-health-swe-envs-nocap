# Issue

**Title:** fix(backend): page recovery summaries by day, not by score row

## Description

## What does this change?

`/summaries/recovery` now pages by day, so a page holds `limit` days and `has_more` is right when a day has more than one recovery score.

## Why?

This is the recovery half of #1831. `get_recovery_summaries` applies the cursor and `limit + 1` to the raw score rows, then `_filter_by_priority` keeps one score per day, and only after that does the service check `has_more`. Any day with more than one score breaks that.

It's more common than it looks. Suunto stores one recovery score per Balance sample (`suunto/data_247.py:466`), which is every half hour going by third party docs for their API, so a Suunto user on their own gets 2 days back from a 50 item page with `has_more: false`. Users with two of WHOOP, Polar, Suunto and SensorBio hit it too, since all four write recovery scores (`whoop/data_247.py:753`, `polar/data_247.py:602`, `suunto/data_247.py:439`, `sensorbio/data_247.py:458`). The route docstring and #1461 say only WHOOP does, so I wanted to mention that.

The repository now picks the next `limit + 1` days first and then loads each source's earliest score on those days, which is the one `_filter_by_priority` keeps for that source anyway. So the limit counts days, a day never gets split across pages, and a page loads at most one row per source per day instead of every Suunto sample. The cursor format doesn't change. It's the same idea as activity paging by whole days, just done in one query since recovery is stored rows.

I saw #1461 plans to rebuild this endpoint from `data_point_series`. That version will still pick one source per day, so it'll need to page by day as well. If the rewrite is close, feel free to close this.

## How did you test this?

Ran the API locally against Postgres 18 and paged `GET /api/v1/users/{id}/summaries/recovery` with an API key, following `next_cursor` to the end. One user had WHOOP and Polar scores on Jan 2 to 6 (default priorities, so Polar wins), and another was Suunto only with 48 samples a day on the same days:

```
                         main                       this branch
WHOOP+Polar, limit=1     Jan 2, has_more=false      Jan 2 to 6, one per page, all polar
WHOOP+Polar, limit=2     Jan 2-3, has_more=false    Jan 2-3, 4-5, 6, all polar
Suunto only, limit=2     Jan 2, has_more=false      Jan 2-3, 4-5, 6
Suunto only, limit=50    Jan 2-3, has_more=false    Jan 2 to 6
```

Depending on row order, main can also summarise a day cut at the page edge from the lower priority provider. One of my runs returned Jan 3 from WHOOP.

New service tests page forward with limit 1 and 2 and check the previous cursor with two providers per day, and a new API test covers a Suunto user with several samples a day and no data source, checking each day uses its first sample. All 4 fail on main. The full backend suite passes (3108 passed, 3 skipped), ruff is clean, ty shows the same 7 otel import errors as main, and the OpenAPI check is clean.

With 48 Suunto samples a day over 60 days and 20 users in the table, the default page takes about 30 ms here against 18 ms on main, which returns 2 days instead of 50.

Backward pages still come back newest first, and following `previous_cursor` twice repeats a day. That's the same on main and in sleep, so I left it for a separate fix.

## AI usage

Claude Code (Claude Opus) helped trace the bug, write the fix and tests, and draft this description. I reviewed the change and ran the checks above.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Bug Fixes**
  * Recovery summaries now show one selected score per day, prioritizing configured providers and device types, then the recorded time.
  * Pagination now returns consistent daily summaries across pages, including when multiple scores are recorded on the same day or a score has no associated data source.
  * Forward and backward pagination correctly return the selected daily results without repeating dates across pages.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `59520d359e5c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.