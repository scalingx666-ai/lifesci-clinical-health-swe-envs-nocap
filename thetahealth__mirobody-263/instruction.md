# Issue

**Title:** contracts: stop naming two collect modules that no longer exist

## Description

## Summary

`main` is red since `ef8008e6` (#262): **test-build** fails with `Module 'mirobody.collect.readings' does not exist.` The test suite itself passes; the failure is the import-linter step.

import-linter 2.16, released after main's last green build, fails the whole run when a contract names a module that does not exist (2.15 ignored it). The collect front-door contract in `pyproject.toml` still listed `mirobody.collect.backfill` and `mirobody.collect.readings`, both removed on 2026-09-20 by "collect: one writer, one reader" (28f24bb3), when every write moved to `observations.ingest` and every read to `query.py`.

This removes the two names. The comment that used `readings.py` as its example now uses `query.py` and says why every listed module must exist. Nothing else references either module. Not user-visible, so no CHANGELOG entry.

## Testing

- `lint-imports` with import-linter **2.16** against this branch's source: 6 contracts kept, 0 broken (before the change: `Module 'mirobody.collect.readings' does not exist`).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ef8008e6fe5f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.