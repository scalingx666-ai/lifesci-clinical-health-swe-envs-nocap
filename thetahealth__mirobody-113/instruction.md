# Issue

**Title:** ci: upgrade GitHub release action runtime

## Description

## What changed

Upgrade `softprops/action-gh-release` from `v1` to the supported `v3` Node 24 runtime. actionlint had flagged the old action as obsolete after the merged Docker workflow work.

## Validation

- `actionlint .github/workflows/*.yml`
- `ruff check mirobody examples`
- `compileall`
- `lint-imports` — 6 contracts kept, 0 broken
- `pytest -q mirobody/tests/test_skills.py tests/test_doc_paths.py` — 90 passed

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b65abfd47e6c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.