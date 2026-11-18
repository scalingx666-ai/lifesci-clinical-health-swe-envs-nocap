# Issue

**Title:** query: count "the last N days" as N days, both ends inclusive

## Description

## The defect

`query_health_indicators` takes `start` and `end` as inclusive local dates. Asked about "the last N days", the model passed `start = today − N`, so the tool read N+1 days: "the last 60 days" read 61, and the answer said "61 of the last 61 days". Found by a local evaluation.

## The fix (as merged)

The only change in behaviour is the `start` description in `kernel/query.py::TOOL_SCHEMA`, which the chat tool and the MCP tool both publish. It now says both dates are counted and gives a worked example: on 2026-03-10 the last 7 days start 2026-03-04, not 2026-03-03.

`mirobody/tests/test_last_n_days_window.py` checks that example against `resolve_window`, along with the N−1 rule for 1, 7, 14, 30 and 60 days. `docs/answers.md`, `docs/site/health-data-tools.md` / `.zh-CN.md` and the CHANGELOG state the same rule.

**Follow-up:** a worked example fixes the convention, not the arithmetic. Asked about the last 60 days, a local 2B model read about a month. A follow-up PR adds `days=N` so the server does the subtraction. It was pushed to this branch after the merge, so it is not part of this PR.

## Gates (on the merged commit)

ruff clean · compileall ok · `pytest -q` 1257 passed, 121 skipped, 12 xfailed · lint-imports 6 kept, 0 broken · library-layer import ok

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b76f43ea1479`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.