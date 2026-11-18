# Issue

**Title:** tools: keep truncation advice valid across record tools

## Description

When rendered medication logs exceed 40,000 characters, the shared cut notice
tells the model to retry with `view=stats`. `query_medications` rejects that view
because it supports only `plan`, `log` and `history`.

Replace the shared advice with a request to narrow the query using the producing
tool's supported filters. Add a regression through the real `MedicationsService`
with 200 synthetic dose events and in-memory stores; it checks any view suggested
by the notice and preserves complete source metadata for Python calculations.
The test skips when the clock's optional configuration dependencies are absent,
keeping the minimal install supported. The Unreleased changelog records the behavior change.

Validation:

- The new regression fails on the original unsupported `stats` advice and passes
  after the fix; the existing leading character-cut warning regression also passes.
- Full source pytest with disposable local PostgreSQL 17: **775 passed, 12 xfailed**.
- Fresh `.[test]` install: **432 passed, 170 skipped, 12 xfailed**; the application
  case skips rather than importing undeclared configuration dependencies.
- `ruff check mirobody examples`, `python -m compileall -q mirobody` and Python 3.12
  bare library imports pass.
- `lint-imports --no-cache`: **6 kept, 0 broken**.

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d8463a4a190b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.