# Issue

**Title:** resolve: CHOL, Height and Systolic keep their analyte

## Description

Three common report names resolved to a different test with full confidence:

| Name | 1.5.7 | Now |
|---|---|---|
| `CHOL` | 13457-7 Cholesterol in LDL, by calculation | 2093-3 Cholesterol (14647-2 with mmol/L) |
| `Height`, `Height (cm)` | 15286-8 Kidney - left Height by US | 8302-2 Body height |
| `Systolic`, `Systolic (mmHg)` | 24372-5 Peak systolic BP during right ventricular septal defect | 8480-6 Systolic blood pressure |

Each index key posts rows of other tests: `chol` posts 178 rows in which LDL, HDL, total cholesterol and their ratio tie on commonness; `height` posts only organ heights by ultrasound; `systolic` posts one echo measurement. The fix is override rows, as the file's header asks. `总胆固醇(CHOL)` and `Total Cholesterol (CHOL)`, refused as two analytes before, now resolve too.

Once `CHOL` is total cholesterol, the trailing-token guard no longer cuts `LDL-CHOL` to `LDL`, because the halves now differ. So `LDL-CHOL`, `HDL-CHOL` and `CHOL-LDL` get their own rows. They are hyphenated on purpose: a spaced row would also catch the slash spelling `CHOL/HDL`, which is the ratio. Two spaced spellings that 1.5.7 reached only through the wrong CHOL answer, `LDL CHOL` and `CHOL LDL`, now resolve to nothing. `Diastolic`, which resolved to nothing, gets a row beside `Systolic`.

Verified:
- `mirobody/tests/test_engine_coverage.py`: eight new cases. With them, 1.5.7 scores 338/345 and this branch 345/345. `test_every_override_row_does_its_job` passes.
- `benchmarks/run_eval.py` on the 7,354-case held-out set: output identical to 1.5.7 in every stratum.
- Every alias-source term and target, every eval term and reading, and generated compounds of the changed keys (35,421 inputs) resolved before and after. Only the generated compounds move.
- A local regression test (44 cases: new codes, unchanged neighbours, readings with units, no slash ratio landing on one component): 21 fail on 1.5.7, all pass here.
- `test_cross_language_identity.py`, `test_resolver_regressions.py`, `ruff check` and `scripts/check_comment_style.py` pass. `stamp_bundle_version.py --check` passes.

CHANGELOG: this branch opens an `## Unreleased` section. Five sibling fix PRs from the same review do the same, so each one merged after the first needs its entry moved into the existing section; no other file conflicts (all six were merged together in a scratch branch).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a66a4f6654f2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.