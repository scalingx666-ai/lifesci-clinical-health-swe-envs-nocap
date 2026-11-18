# Issue

**Title:** fix: preserve active PR checks when unrelated labels are added

## Description

Adding an ordinary issue label to a PR currently cancels its useful CI run: workflow concurrency runs before the job-level `full-ci` label conditions, so the replacement then skips every job. This reproduced on #4334 when its issue labels were applied; the cancelled compatibility matrix left a failed aggregate gate.

Scope: the maintainer-requested CI queue repair following #4331 and #4333; unblocks the reviewed v3.2 batches in #3195.

## Changes

- Give unrelated label events a unique run-owned concurrency group and disable cancellation for those events.
- Keep normal PR commits and `full-ci` label additions in the PR-owned group so they still replace superseded work.
- Extend the existing workflow contract and document the behavior; no test functions or dependency changes are added.

## Validation

- Full offline suite: 20,401 passed, 177 skipped, 11,209 subtests passed (`.venv/bin/python -m pytest tests/ -q -n 8 --tb=short --show-capture=no`).
- Existing workflow contract: 18 passed, 16 subtests passed.
- `make format`, `make lint`, `make format-check`, `actionlint`, pinned Actions-reference policy, `uv lock --check`, and frozen dev/docs sync passed.
- Strict docs staging and wheel/source builds passed.
- Existing high-severity Bandit gate passed; pip-audit found no known vulnerabilities.

No library runtime code, release publishing policy, or test-tier selection changes.

Hosted label regression verified on this head: applying `bug`, `P1` and `roadmap-v3` produced three skipped label-only runs while the original [CI run](https://github.com/maziyarpanahi/openmed/actions/runs/40939185783) remained queued. The useful run was preserved.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f501e83e4fb6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.