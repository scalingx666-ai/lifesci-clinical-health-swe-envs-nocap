# Issue

**Title:** fix: preserve Apple daily figures during re-import recalculation

## Description

Apple Health re-imports could retract valid published daily figures in two cases: an aggregation failed and returned incomplete results, or a 30-day chunk skipped its first day's earlier samples. Both cases were reproduced against PostgreSQL on the 1.6.0 release candidate.

This change:

- Requires complete computation before a sweeping recalculation writes or retracts any daily figures. Person-day and custom derived failures return an error to the importer; previously published figures remain visible, and a retry completes the timezone repair. The incremental worker continues isolating failures by person and day.
- Aligns inclusive date ranges to midnight before splitting them, so consecutive chunks cover every calendar day.
- Publishes ten regression cases: seven database cases covering first-day/partial-result failures, driver-message privacy, retry recovery and 29/35/65-day import/re-import coverage, plus three application cases for incremental error isolation and custom derived failures.
- Updates the changelog (both entries in 1.6.0's Fixed list, after the Apple entries they make safe), aggregation/pipeline documentation and test counts (`docs/testing.md` re-measured per extra: `[test]` 833/244/12, `[test,parse]` 919/232/12, `[test,app]` 1190/150/12; 1622 collected). No README editions changed.

Before the fix, the failure reproduction reduced nine visible daily figures to zero while reporting success; an unchanged 35-day re-import reduced its daily coverage to 34 days. The new tests require the previous figures to survive failure and every supported day to survive an unchanged re-import.

Targets `release/1.6.0`: merge this before merging #264 and tagging 1.6.0.

Validation on Python 3.12 with a disposable PostgreSQL 17 database and synthetic fixtures:

- All tracked tests: **1610 passed, 12 xfailed, zero skipped**. Executed against checkout source with only tracked test files; this machine also has obsolete gitignored maintainer tests referencing removed modules, which were excluded.
- Targeted regression/Apple day tests: **13 passed**. The ten new cases skip cleanly on a minimal `[test]` install.
- `ruff check mirobody examples benchmarks/windows`, `compileall`, `lint-imports` (**6 kept, 0 broken**), bare-interpreter kernel imports, version consistency, comment style, PHI baseline and `git diff --check`: passed.
- Published genomics and health-record benchmarks: passed (the genomics suite retains its two expected skips).
- `scripts/e2e_health_data.py` against the disposable database with synthetic readings: **0 failed**; the PHI canary did not reach captured logs. This exercised the native database/tool path, not a newly built HTTP container.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a87ef50e4f8a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.