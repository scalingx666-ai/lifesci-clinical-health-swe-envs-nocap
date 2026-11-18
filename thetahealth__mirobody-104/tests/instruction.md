# Issue

**Title:** release: 1.5.3

## Description

Cuts 1.5.3 from main (#102): the version literal, `server.json` and the CHANGELOG heading. No code changes.

Verified on this tree:
- Full local suite: 2,999 passed, plus the genotype corpus module (93) and the 56 database-backed tests against a scratch Postgres
- The shipped tests (134 passed + 13 strict xfails), including on a minimal `[test]` clone install
- The wheel and sdist build; `check_wheel_data`, twine
- The three wheel gates in fresh venvs: numpy-only library, `[parse]` without FastAPI, a langchain-free server install
- lint-imports (6 contracts), ruff, comment style, bundle stamp
- e2e five stages on the local stack: see the comment below

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `47340208f1b5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.