# Issue

**Title:** collect: keep a dimensionless value's last digit

## Description

With the UCUM unit `1` (INR, specific gravity, ratios), `collect.query._shown` read a value's final digit as a repeated unit and dropped it. On 1.5.7, `_shown("1.021", "1")` returns `1.02`, `"2.31"` returns `2.3`, `"11"` returns `1` and `"-21"` returns `-2`. Raw, latest, catalogue and statistics rows share this function, so the model and the UI saw a wrong number.

A unit that starts with a digit is now removed from a value cell only after a printed space. `11 1` still shows `11`, and `170 ms`, `170ms` and `11%` behave as before.

Verified:
- New local regression (root `tests/`, not shipped): 12 cases. 5 fail on 1.5.7; all pass with the fix.
- Local `tests/collect/test_query.py`: the fix clears 4 failing display cases (`11`/`1`, `-21`/`1`, `110*9/L`/`10*9/L`, every reading projection). All other results are identical before and after.
- `ruff check mirobody examples benchmarks/windows` and `scripts/check_comment_style.py mirobody` pass.

CHANGELOG: this branch opens an `## Unreleased` section. Five sibling fix PRs from the same review do the same, so each one merged after the first needs its entry moved into the existing section; no other file conflicts (all six were merged together in a scratch branch).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b5c7df8da87e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.