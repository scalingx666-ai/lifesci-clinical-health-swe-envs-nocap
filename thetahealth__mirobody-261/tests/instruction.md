# Issue

**Title:** fix: prefer fresh Apple Health transport data for a day

## Description

## What this changes

Daily summaries can show an older Apple Health total even after newer measurements arrive through another transport. The stale value also appears in trends and agent responses. The election ranked coverage ahead of measurement freshness, allowing an older export with broader coverage to beat a newer push. Generated summaries have synthetic time boundaries, so their timestamps do not establish when the underlying samples were measured.

For generated summaries, valid push, export and watch streams first elect one Apple representative by source class, actual sample freshness, coverage and priority. Freshness uses valid numeric samples from the same source-ID selection and time window as aggregation; missing evidence preserves the existing ranking. The representative then competes with other vendors under the ordinary policy, without adding transport totals together. Authority records also update when the election rule changes.

Ran `./scripts/fetch_data.sh` locally on macOS for the mirobody elect_day change; it passed.
The `python_tests` check found no tests to run, so it provides no regression-test validation.
Ran `./scripts/fetch_data.sh` in a Linux container (`python:3.12`) for the mirobody elect_day change; it passed.
Ran `./scripts/fetch_data.sh` locally on macOS for the mirobody elect_day change; it passed.
The new test mirobody/tests/test_apple_transport_election.py did not run here: no test runner for it was available.

## Which gate you ran

- [ ] `pytest -q` (full local suite, both roots)
- [ ] `pytest -q mirobody` (what a clone runs)
- [x] `lint-imports` — required for anything touching `mirobody/kernel`, `mirobody/engine/` or `agent/`
- [x] `uvx ruff check mirobody examples`
- [ ] `python -m benchmarks.run_eval` — required for any resolver or bundle change

## Which benchmark it moves

Not applicable to this change.

AI was used for assistance.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6aa3f98111ac`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.