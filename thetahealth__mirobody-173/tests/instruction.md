# Issue

**Title:** bench: grade sleep as durations and device values by precision

## Description

The 100-question local suite failed correct answers because of how it compared numbers.

- **Sleep.** Totals and means were checked in minutes with a 0.1 tolerance, so "47.6 hours" or "2858 minutes" for 2858.25 failed. Where the question doesn't fix the unit (`sleep-observed-total`, `conversation-4-start`), these are now `duration` facts that accept hours, h+min or minutes, within 3 min. That is the rounding error of a one-decimal hours answer. The two questions that ask for hours stay numbers, with a 0.05 h tolerance.
- **Device tolerances.** Each value now allows half the step it is normally stated in: 1 for steps, mmHg and bpm; 0.1 for kg, lb, hours and percent. Any correct rounding passes (9586 for 9585.57, 78 for 77.67, 82 for 81.67), but a neighbouring reading such as 112 for 113 still fails. A difference between two means allows a whole step. Lab tolerances are unchanged.
- **Suite ID.** The suite is now `harness100-20261023`. The questions and the loaded record are unchanged (`record_identity` is the same), so the accounts keep the `harness100-20261021` name. `cases.jsonl` and `plan.json` were regenerated from mirobody-gen 9723605, and `cases.py --check` passes.

Tests: `test_local_eval_contract.py` now pins hours, h+min, minutes and integer-rounded answers as passing and clearly wrong values as failing. Gates: ruff clean, compileall OK, lint-imports 6 kept / 0 broken, pytest 800 passed / 107 skipped / 12 xfailed.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7775b50a55e1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.