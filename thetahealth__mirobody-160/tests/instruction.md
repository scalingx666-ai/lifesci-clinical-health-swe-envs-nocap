# Issue

**Title:** collect: keep subsecond reading times

## Description

Raw readings, latest values and the records list format a reading's local time with `to_char(..., 'YYYY-MM-DD HH24:MI:SS')`. Distinct device samples within one second, such as an intraday heart-rate stream or a burst of uploads, are therefore shown at one identical instant, and the latest view's `ORDER BY local_time` cannot tell them apart.

The time now keeps PostgreSQL's microseconds with trailing zeros trimmed (`2026-06-01 12:00:00.000001`, `… 12:00:00.5`). A whole second still reads `2026-06-01 12:00:00`, and bucket periods are unchanged. Trimmed fractions sort correctly as text within a second, so the latest view's ordering stays consistent. `docs/answers.md` states the format.

Verified against a disposable PostgreSQL 16 (pgserver):
- New case in the shipped `mirobody/tests/test_postgres_regressions.py`: 12 instants from 0 µs to 1.000001 s, 5 zones (fixed offsets and DST zones), through `readings`, `latest` and both `records` paths. All 5 parametrizations fail on 1.5.7 and pass with the change.
- Whole module before: 94 passed, 10 failed. After: 99 passed, 5 failed. The 5 remaining failures are pre-existing `ModuleNotFoundError: fastapi` in this environment (no `[app]` extra) and occur on both.
- `ruff check mirobody examples benchmarks/windows` and `scripts/check_comment_style.py mirobody` pass.

Risk: `local_time` gains a fractional part when a reading has one; a client that parses it strictly as `YYYY-MM-DD HH:MM:SS` would need to accept the fraction.

CHANGELOG: this branch opens an `## Unreleased` section. Five sibling fix PRs from the same review do the same, so each one merged after the first needs its entry moved into the existing section; no other file conflicts (all six were merged together in a scratch branch).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d6dd54da1c3a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.