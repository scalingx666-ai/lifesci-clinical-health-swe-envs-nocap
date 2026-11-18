# Issue

**Title:** onboarding: four ways in, and Codespaces without Docker

## Description

## What this changes

The README opens with four ways in instead of one, and Codespaces runs Mirobody
without Docker: PostgreSQL and pgvector come from the container's own packages,
so nothing is pulled from a registry. Verified in a real codespace end to end:
~4 min to provision, the app up on container start with nobody running anything
by hand, health 200, the client served, the demo seeded (2 accounts, 2019
readings), a PDF upload extracting into three new indicators, and an agent
answer with citations.

Also here: Turkish all-caps names resolve (discussion #137), `deploy.sh` tries
`mirror.gcr.io` first and probes with the database image, and
`docs/quickstart.md` no longer claims `mirobody dev` cannot serve the web client
from a checkout.

## Which gate you ran

- [x] `pytest -q mirobody` — 372 passed, 13 xfailed
- [x] `lint-imports` — 6 kept, 0 broken
- [x] `uvx ruff check mirobody examples` — clean
- [x] `python scripts/check_comment_style.py mirobody` — 0 problems
- [x] `python -m benchmarks.run_eval --testset <private>` — see below
- [ ] `pytest -q` (full local suite, both roots) — not run; this checkout has no root `tests/`

## Which benchmark it moves

None: 7,354 cases, coverage 0.916, precision 0.969, recall 0.887, wrong-rate
0.030 — identical before and after. The Turkish cases live in
`test_engine_coverage.py`, whose score went 321/321 to 325/325 with the four
all-caps cases pinned.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fc4b8072cd24`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.