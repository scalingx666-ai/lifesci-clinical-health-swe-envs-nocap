# Issue

**Title:** docs: make quickstart paths independently runnable

## Description

## Summary
- Make the library, Docker, and source checkout paths independently usable from the open-source quickstart.
- Correct the Postgres user in the checkout example and in the CLI's missing-database hint.
- Point the hosted link to the separate Cloud quickstart and run Docker diagnostics inside the container.

## Verification
- `ruff check mirobody examples` — pass using the repository Python 3.12 environment.
- `python -m compileall -q mirobody` — pass.
- `python -m pytest -q` — 134 passed, 13 expected failures.
- `lint-imports` — 6 contracts kept, 0 broken.
- Bare interpreter imports and `git diff --check` — pass.
- `python -m mirobody dev` without a database displays the corrected Docker hint.

The documentation site's generated English quickstart will be synchronized from this commit after merge.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `934f41b6050d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.