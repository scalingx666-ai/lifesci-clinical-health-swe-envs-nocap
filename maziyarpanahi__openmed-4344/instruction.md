# Issue

**Title:** feat: add synthetic FHIR and OMOP fixtures

## Description

## Description

Consolidate Rudy Celekli’s structured synthetic fixture work into one reviewed change. FHIR collection fixtures have closed, typed references and source-bound provenance; OMOP-shaped rows have coherent foreign keys, visit chronology and independently computed cohort truth. These offline fixture subsets do not claim full FHIR/OMOP conformance or clinical validation.

## Included pull requests

- #4191 — referentially closed synthetic FHIR records
- #4195 — synthetic OMOP rows and cohort truth

## Type of change

- New optional synthetic-data APIs; no new dependencies.

## Maintainer integration changes

Updated both branches from current master, preserved their contributor history and reconciled only changelog, navigation and publication metadata. The actual integration tree matches the passing local rehearsal exactly.

## Validation

Exact final head `9f548929306c4d5b209efd1bf57075cad26a4386`: **21,353 passed, 177 skipped, 11,209 subtests passed** in 181.52s. The 26 focused checks, `make format`, `make lint`, `make format-check`, strict `make docs-build`, three Chromium artifact-budget/marketing-beacon/clinical-exclusion checks, wheel/sdist build and both packaged-module byte comparisons passed. The actual integration tree equals the passing rehearsal. Hosted lint, repository policy, lockfile drift, secret scan and available compatibility/build checks have passed; other hosted jobs remain queued or running, with no failures observed. Master has no required check contexts; the complete exact-head local suite supplies validation for the queued Python jobs. No new dependencies or mandatory network calls/model downloads were added. Documentation and Unreleased notes are included.

## Issues resolved

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6a7e00887790`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.