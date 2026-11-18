# Issue

**Title:** collect: mixed-unit means keep precision and one basis

## Description

A series may hold readings in two units, and `stats` and the bucket views then aggregate the canonical values. On 1.5.7 that gives wrong numbers in two ways (measured on PostgreSQL 16, two synthetic readings per series):

| Series | 1.5.7 avg | True mean |
|---|---|---|
| Creatinine 80 umol/L, 0.9 mg/dL | 0.0001 mol/L (100 umol/L) | 7.978e-05 mol/L |
| Bilirubin 17 umol/L, 1.0 mg/dL | 0.0 mol/L | 1.705e-05 mol/L |
| Uric acid 350 umol/L, 6.0 mg/dL | 0.0004 mol/L | 3.535e-04 mol/L |
| Albumin 40 g/L, 600 umol/L | 20.0003 "mol/L" | none: g/L and mol/L |
| 25-OH vitamin D 50 nmol/L, 25 ng/mL | 0.0 "mol/L" | none: g/L and mol/L |

1. `ROUND(avg, 4)` ran on base-unit values, where four places are too few.
2. With no molar mass, the canonical values of one group stay in g/L and mol/L. The aggregate mixed them and labelled the result with `MAX(unit_canonical)`.

Now the canonical mean is not rounded, and a group whose numeric readings do not all have a value in one shared canonical unit returns no min, max, avg or unit. The printed-unit path, used when a group has one unit, keeps its four-place mean. `first`, `last` and `count` are unchanged.

Verified against a disposable PostgreSQL (pgserver):
- New case in the shipped `mirobody/tests/test_postgres_regressions.py` (creatinine and albumin through `stats` and month buckets). It fails on 1.5.7 (`0.0001 == 7.97808e-05`) and passes here. Module: 94 passed before, 95 after. The same 5 tests fail on both because this environment lacks `fastapi` and `mandrill`.
- Local checks: a single-unit series keeps min, max, avg 5.38, change and per-day buckets unchanged; mixed glucose averages 5.5753e-3 mol/L (was 0.0056); vitamin D returns no aggregate.
- `ruff check mirobody examples benchmarks/windows` and `scripts/check_comment_style.py mirobody` pass.

Not changed here: in a mixed-unit `stats` row, `first` and `last` are printed values but share the row's single `unit` column, so `first=80, last=0.9, unit=mol/L` still reads as one unit. Fixing that needs per-endpoint units in the output, which is a schema choice for the maintainers.

Risk: a mixed-unit mean is now returned unrounded in base units (for example `7.97808e-05` mol/L); I have not checked how every caller formats it.

CHANGELOG: this branch opens an `## Unreleased` section. Five sibling fix PRs from the same review do the same, so each one merged after the first needs its entry moved into the existing section; no other file conflicts (all six were merged together in a scratch branch).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ad8e7721dfaa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.