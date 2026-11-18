# Issue

**Title:** standardize: expand coverage while preserving measurement identities

## Description

## What changes

Catalogue displays and printed lab/device spellings previously missed their indicators or reached another measurement. This adds 18 chemistry rows, three supported device codes and the display-name bridges, while preserving each reading's identity.

- Serum sodium is `serumSodium`; dietary `sodium` retains its `mg` unit and cumulative shape. Conflicting duplicate catalogue names fail at load time.
- Instantaneous walking speed retains its device identity because LOINC 41956-4 describes a 24-hour maximum.
- Printed BMI, cell-count, pump and energy-unit spellings normalize to UCUM. Competing units such as `mg/dL, mmol/L` are refused.
- Regression checks use raw catalogue rows and explicit six-axis expectations; they allow legitimate specimens outside blood. PostgreSQL tests exercise writing and querying the distinct identities and refusing ambiguous units.

## Validation

Fresh checkout of `10ce4c10`, source imports asserted:

- `python -m pytest -q`: **1257 passed, 12 xfailed**, including **113 PostgreSQL regressions** against a disposable PostgreSQL 17 database.
- Ruff, compileall, all six import contracts and bare library imports passed.
- Minimal Python 3.13 library run: 637 passed, 178 skipped, 12 xfailed.
- Comment, version and PHI gates passed.

## Merge order

**Merge #188, then #190, then #191 using Create a merge commit.** The later branches contain these repaired commits and resolve their overlapping alias/catalogue additions. Existing commits were retained; no force push was used.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5146ccdd3c03`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.