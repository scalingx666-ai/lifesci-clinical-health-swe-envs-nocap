# Issue

**Title:** fix(backend): return 400 for out-of-range numeric date params

## Description

## What does this change?

Out-of-range numeric date params like `inf` or `1e20` now get the same 400 as any other unparseable date, instead of a 500.

## Why?

`parse_query_datetime` tries `float()` then `fromtimestamp()` and only catches `ValueError`, but `fromtimestamp` raises `OverflowError` for these, and nothing handles that, so every route using the parser returned 500. `parse_query_end_datetime` already suppresses `OverflowError` for date-only strings, so this just brings the main parser in line. I raised `DatetimeParseError` directly from the `OverflowError` branch rather than falling through to `fromisoformat`, since the value is clearly numeric and the ISO parse can't succeed.

The fix was small enough that I went ahead with it, happy to change direction if you'd rather handle it differently.

## How did you test this?

`GET /api/v1/users/{id}/summaries/activity?start_date=<value>&end_date=2026-10-12` through the app's test client against the test Postgres:

```
              before (main)   after
banana        400             400
inf           500             400 {"detail":"Invalid datetime format: 'inf'. ..."}
-inf          500             400
1e20          500             400
2026-10-01    200             200
```

Also confirmed the `OverflowError` itself on Linux with Python 3.14 (`python:3.14-slim`), same values. New tests in `tests/utils_tests/test_dates.py` (parser, start and end bounds) and `tests/api/v1/test_summaries.py` (route returns 400) fail on main and pass with the fix. `test_dates.py` and `test_summaries.py` pass in full, ruff and ty are clean.

Not tested: I didn't bring up the full docker-compose stack and curl it, the requests above went through the FastAPI test client.

## AI usage

Claude Code (Claude Opus) helped trace the bug, write the fix and tests, and draft this description. I reviewed the change and ran the checks above.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Bug Fixes**
  * Invalid or excessively large date values now return a clear validation error instead of causing an unexpected failure.
* **Tests**
  * Added coverage for invalid date values in date parsing and activity-summary requests.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d07f0d534051`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.