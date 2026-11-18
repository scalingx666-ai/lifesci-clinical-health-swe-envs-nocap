# Issue

**Title:** tools: an empty window says it is empty, and which cause it is

## Description

## What was wrong

An empty answer to a named window has two causes: the selection matched no series, or it matched series that have nothing in the window. `_run` sent both to the catalogue fallback under "no indicator matched those terms", and added "no data for an indicator means it was never recorded". Both statements are false for a series the record holds outside the window. Answering PHIA's objective set, a local 2B concluded exactly that in 11% of its failures.

The first version of this PR put its note in the `elif not rows:` branch of `_envelope_for`. The tool never reaches that branch, because the fallback always runs first, so the note never reached a model. Its tests called `_envelope_for` directly and passed anyway.

## What changed

- **Empty named window:** `_run` reads the selection's whole-record `stats` before falling back.
- **Selection matched:** the answer is zero rows with `0 readings between <start> and <end>`, plus each indicator's count and its first and last dates. There is no "never recorded" note and no `pick_from_catalog`.
- **Selection matched nothing, or no dates were named:** behaviour is unchanged (the catalogue fallback).
- **Cost:** the extra query runs only when a dated window comes back empty. The whole-record outside-window note is now skipped when there are no rows to compare.

## How to tell

- `mirobody/tests/test_absence_semantics.py` drives `envelope()`, the real entry point: a series held outside the window, a selection that matches nothing, an undated empty answer, and a window with rows.
- A Postgres case in `test_postgres_regressions.py` runs the real store.
- `pytest -q` passes, with PostgreSQL 17 (1326 passed, 12 xfailed); so do ruff, the comment-style check and `lint-imports`.
- Merged with #206 onto main: 1342 passed. The two PRs conflict only where both append, in `CHANGELOG.md` and at the end of `test_postgres_regressions.py`; keep both sides.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a5dd75328a1a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.