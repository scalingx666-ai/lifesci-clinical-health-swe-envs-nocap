# Issue

**Title:** query: stats carry sum; a character cut says so

## Description

## What was wrong

- **No sum in stats.** `view=stats` returned count/min/max/avg but no sum. A total over more readings than the raw view returns (`query.ROW_CAP`, 50 per indicator), such as a year of exercise logs, could only be rebuilt as avg × count, which a model rarely did.
- **A character cut read as complete.** A rendering cut at `MAX_RENDER_CHARS` (40,000) was announced only after the rows, with `… cut at 40000 characters`, and the meta line still read as complete. A model summed the rows it could see.

## Fix

- Stats carry `sum` over the same values and unit as `avg` (`_STAT_VALUE.format(agg="SUM")`). It is added to the stats columns, the tool schema's `view` description and `docs/answers.md`.
- A character cut is stated before the rows. The statement says how many lines fit and points to `view=stats` for totals and averages. The meta line now reads `truncated`.

## Tests

- `test_collect_regressions.py::test_a_rendering_cut_by_characters_says_so_before_its_rows`.
- `test_postgres_regressions.py::test_stats_sum_is_the_total_over_every_reading_of_an_unelected_day`.
- Engine suite (`mirobody/tests` without the PostgreSQL module): 411 passed, 62 skipped, 12 xfailed.
- PostgreSQL module against a disposable pgserver:
  - main 6944beb1: 101 passed, 5 failed;
  - this branch: 102 passed, 5 failed.
  - The same 5 fail on both: they need `fastapi`, which is not installed in the test environment.
- `ruff check mirobody examples` is clean.

Found during the same fidelity audit as #156–#162. Merging is the owner's call.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6944beb10008`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.