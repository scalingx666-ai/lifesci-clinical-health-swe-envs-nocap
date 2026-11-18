# Issue

**Title:** query: express a value band so a counting question can be answered (no prompt hint)

## Description

## The question

*"How many days in the past week did I get less than 1 hour of deep sleep?"* is a value band plus a count. The tool returned the whole series and left both to the model; a local 2B answered `30.75`, a duration.

## What this adds

- `value_min` / `value_max` with `view="stats"`. Stats rows carry `days` (distinct local days) and, when a band is given, `count_in_range` (readings in the band) and `days_in_range` (days with at least one reading in it).
- The schema names `days_in_range` as the answer to "how many days". It says the bound is in the unit the stats row reports: sleep durations are in ms, so "under an hour" is `value_max: 3600000`.

## Fixed after review

- **Unit basis.** The band compared printed values, while min/max/avg compare canonical ones when units differ: 80 umol/L counted and 0.9 mg/dL did not, the same creatinine, in a row reported in mol/L. The band now uses the row's own basis. A series with no shared unit gets no count.
- **Pieces are not days.** A series stored in pieces gets no band count, with a note naming its daily series. These are the catalogue codes whose every row is cumulative, interval or session: steps as increments, sleep as segments. Three 4,000-step readings had counted no day above 10,000.
- **Bad bounds are refused.** A bound that is not a finite number (`"abc"`, NaN, inf, a boolean), or a `value_min` above `value_max`, is refused. Before, it was ignored and every reading counted as in the band.
- **Other views say so.** A band on a view that does not count is answered as asked, with a note saying the band was not applied. This follows `view_unapplied`, rather than refusing into a retry loop.
- **No band, no band columns.** `count_in_range` / `days_in_range` are `None` without a band, so they are not rendered.
- **Store compatibility.** `HealthQuery.stats` takes the band as optional keyword arguments, passed only when given, so a store written before this keeps working.
- **Tests.** The source-text assertion is replaced by Postgres cases: counts and days on one unit, creatinine on the canonical basis, albumin with no shared unit, and steps through the service.

## How to tell

- `pytest -q` passes, with PostgreSQL 17 (1337 passed, 12 xfailed); so do ruff, the comment-style check and `lint-imports`.
- Merged with #207 onto main: 1342 passed. They conflict only where both append, in `CHANGELOG.md` and at the end of `test_postgres_regressions.py`; keep both sides.

## Not covered

Whether the agent reaches for the band is still the capability being measured: no prompt points at it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `849a8c47586d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.