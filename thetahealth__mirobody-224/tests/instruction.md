# Issue

**Title:** meds: count "the last 30 days" as 30 days, quote the N-1 example

## Description

## The defect

`query_medications` takes `start` and `end` as inclusive local dates, like `query_health_indicators`. It had two problems:

1. **Its default was 31 days.** With no dates, `view="log"` is published as "the last 30 days". `_window` built it as `today − 30 … today`, and both ends are counted, so it read 31 days. A call with only `end` also read the 31 days ending there.
2. **`start` said "inclusive" and nothing else.** That is the wording under which a model wrote the readings tool's "last N days" as `today − N`. #223 fixed this for readings with a worked example; the medications tool did not have it.

## The fix

The tools' parameters are unchanged.

- **The window** (`agent/tools/medications_service.py::_window`): the default dose log and the `end`-only window now start N−1 days back. On 2026-06-10, `view="log"` reads 2026-05-12 … 2026-06-10. The `end`-only fallback uses `meds.LOG_DEFAULT_DAYS` instead of a second literal `30`; the value is the same.
- **The worked example** (`kernel/query.py`): the sentence #223 put in the readings `start` description is now one constant, `query.LAST_N_DAYS_EXAMPLE`. The readings schema is byte-identical to main. `meds.TOOL_SCHEMA["properties"]["start"]` quotes the same constant, and its "(default: the last 30 days)" is now read from `LOG_DEFAULT_DAYS`, so the text cannot disagree with the code.

What callers will notice: `query_medications(view="log")` with no dates now returns one day less. The day it no longer reads is the one 30 days ago.

## Tests

`mirobody/tests/test_last_n_days_window.py` (from #223) now also checks:

- both tool schemas carry the example in `start`;
- the dose log asks its store for exactly 30 days with no dates, for the 30 days ending on an `end`-only date, and for an explicit window unchanged. It also reports that window, and each window is measured with `resolve_window`, the readings tool's arithmetic.

The default and `end`-only cases fail on the old `_window`.

**Maintainers' local suite:** `tests/agent/tools/test_medications_service.py:118` pins the old 31-day window, `(date(2026, 5, 11), TODAY)`. It needs `(date(2026, 5, 12), TODAY)`. I ran that file and `tests/test_meds.py` against this branch: 99 pass, and that one fails as expected.

## Docs

Only the places that state the default: `docs/medications.md`, `docs/answers.md`, `docs/site/medications.md` and `.zh-CN.md`. CHANGELOG has an Unreleased entry.

## Gates

Run from this branch, with the worktree on `PYTHONPATH`:

- `ruff check mirobody examples`: all checks passed
- `python -m compileall -q mirobody`: ok
- `pytest -q`: 1293 passed, 121 skipped (database), 12 xfailed
- `lint-imports`: 6 kept, 0 broken
- `python3 -c "import mirobody.kernel.meds, mirobody.kernel.query"`: ok, also in a Python 3.12 interpreter with only numpy installed

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d3017a20f630`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.