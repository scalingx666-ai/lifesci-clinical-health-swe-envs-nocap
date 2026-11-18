# Issue

**Title:** Fix globulin observation units to match existing g/dL ranges

## Description

.

Change seven LOINC `10834-0` unit labels from `g/L` to `g/dL` across five modules, matching their existing `2–3.5` numerical range. Add a parameterized test that executes all seven affected production panels and the already-correct gallstones panel as a control; numerical ranges and sampling are unchanged.

`g/L` is a valid unit ([LOINC](https://loinc.org/10834-0)); this fixes the unit/range pairing. [Labcorp's mapping](https://www.labcorp.com/tests/001487/protein-electrophoresis-serum) also uses `g/dL` for this code.

### Validation

- Before the fix: seven new regression cases fail on the unit assertion; the control passes. After the fix: all eight pass.
- Native Gradle `check`, JDK 17.0.19 / Gradle 9.2.1: 657 tests, 651 passed, six skipped, zero failures or errors.
- Deterministic execution of the eight panel states through the production FHIR R4 and CSV exporters: 128 observation values unchanged in each format; only the seven expected globulin units change. The control is unchanged.
- Structural comparison: exactly seven production unit fields changed in five files. Patch application against pristine `d9d07a6e` reproduces the tested files.

The full check ran in an ASCII-only checkout to avoid an existing flexporter fixture-path encoding issue. Checkstyle reports one existing line-length warning in unchanged `App.java:47`, with no test violations.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d9d07a6eef91`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.