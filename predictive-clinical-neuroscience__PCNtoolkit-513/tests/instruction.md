# Issue

**Title:** fix: define y for unwarped BLR.transfer()

## Description

## Summary
- `BLR.transfer()` never assigned `y` when `self.warp` was falsy (the
  default), causing `UnboundLocalError` at the first use of `y`.
- Added the missing `else` branch, matching the existing pattern in
  `backward()` and `elemwise_logp()`.
- Added a regression test (`test_004_transfer_should_fit_when_unwarped`)
  covering the no-warp path, which had zero prior test coverage.



## AI usage
Bug found and fix drafted with AI assistance (Claude Code / Claude Sonnet 5); verified by tracing the code path, confirming BLR()'s default warp_name=None, and running the full test suite locally before submitting.

## Test plan
- [x] `pytest test/test_norm/test_normative_model_transfer.py -v` — all 4 tests pass, including the new regression test
- [x] `ruff check` / `ruff format` run on changed files only

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1197fe3fa97b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.