# Issue

**Title:** catalog: add 209 chemistry indicators by specimen with reproducible LOINC checks

## Description

## What changes

This builds on the repaired #188 and #190 and adds **209 chemistry indicators** from LOINC 2.83 Universal Lab Orders. Existing serum codes are reused instead of creating a second catalogue identity. The combined catalogue contains **543 members, 534 names and 287 unique LOINC codes**, covering **226 of the 1,519 universal orders**.

- Generation rejects missing, unrecognized or incompatible units and verifies all six axes against the shipped bundle.
- Every generated identity carries its specimen suffix. Name/member collisions are checked after naming, so an existing serum analyte cannot hide urine or CSF siblings.
- Point measurements are `series / instant / last`; 24-hour measurements are `summary / provider_daily / provider_value` with no unsupported aggregation task.
- The generated manifest records each source unit and all six axes. Tests check every row, display and numeric reading, every unit, internal lookup identity and timing. Synthetic releases exercise rejection paths, collisions and reruns.
- Re-running the generator against the combined catalogue emits **zero rows**. English, Chinese and Japanese READMEs and both standardization guides carry the current catalogue count.

## Validation

Fresh checkout of `e4cda9b8`, source imports asserted:

- `python -m pytest -q`: **1278 passed, 12 xfailed**, including **113 PostgreSQL regressions** against a disposable PostgreSQL 17 database.
- Ruff, compileall, all six import contracts and bare library imports passed.
- The health-data end-to-end script ran with synthetic readings and the real writer/query services in an isolated PostgreSQL schema: **0 failed**.
- Python 3.13 minimal library run: 658 passed, 178 skipped, 12 xfailed.
- Genomics benchmark: 37 tests, 2 skipped; health-records benchmark: 3 tests passed.
- Wheel and sdist built; all 29 required data files were present and real, with build-only artifacts excluded.
- Comment, version and PHI gates passed.

## Merge order

**Merge #188, then #190, then #191 using Create a merge commit.** Both catalogue and alias conflicts are resolved, and repeated LOINC rows across the PRs are removed. Original commits are retained.

These checks exercise the resolver, storage and query paths. An agent benchmark run is outside this change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e315ab14d7a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.