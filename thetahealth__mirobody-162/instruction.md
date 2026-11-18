# Issue

**Title:** units: a reading of exactly 1 keeps its number

## Description

## What was wrong

`1` is also the UCUM unity unit. `parse_value_unit` tries the whole input as a unit first (Path A), so a value cell holding exactly `1` came back as `unit="1", value=None`, and `parse_value` stored the reading as narrative.

- `parse_value("1", "mmol/L")` returned `value_kind="narrative"`, while `"1.0"` and `"2"` were quantities.
- Counts included the reading, but means, minima and buckets dropped it: a series 1, 2, 3 counted 3 readings and averaged 2.5.
- In our synthetic probe on release 1.5.7, all 8 of 8 probe series reported a wrong mean, and 65 of 1,046 readings had no number. The defect is unchanged on main 74b931de.

## Fix

A bare comparator+number (`_VALUE_PREFIX.fullmatch`) skips Path A, so it reaches Path B and keeps its value. No other bare number resolves as a unit (`+1`, `-1`, `0`, `10`, `100`, `1.0`, `<1` all returned `None` from `_resolve_strict`), so only an exact `1` changes. The unit column `1` still normalizes to `1`.

## Tests

- `test_engine_coverage.py::test_a_reading_of_exactly_one_keeps_its_number`: fails on main, passes here.
- `test_postgres_regressions.py::test_a_reading_of_exactly_one_enters_the_statistics`: the series 1, 2, 3 gives count 3, mean 2.0, min 1.0. It fails on main.
- Engine suite (`mirobody/tests`, without `[app]`): 410 passed, 167 skipped, 12 xfailed.
- PostgreSQL module against a disposable pgserver: 100 passed and 6 failed before, 101 passed and 5 failed after. The 5 remaining failures need `fastapi` and fail identically on main.
- `ruff check mirobody examples` clean; `compileall` ok; `lint-imports` 6 kept, 0 broken.

Found during the fidelity audit that also produced #156, #158, #160 and #161. The merge is the owner's call.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `74b931de9be6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.