# Issue

**Title:** feat: add artifact-bound multimodal validation packs

## Description

## Description
Add six synthetic multimodal validation packs and an artifact-bound blinded-review workflow for ECG quality/interval candidates, form grounding, DICOM coverage, pixel identifiers, and whole-slide tiling/provenance.

Reviewers score exact source/output/rubric snapshots. Missing or stale evidence is refused; disagreements remain on hold until an independent qualified reviewer adjudicates them. Any observed privacy or provenance failure remains blocking. Public reports suppress small cells and reconstructable overall totals.

The fixtures execute actual component APIs against generated assets. They contain no patient data, external weights, or completed clinician reviews. Simulations remain explicitly labelled; satisfying the rubric is not clinical validation.

## Type of change
- [x] New feature
- [x] Documentation update
- [x] Test addition/improvement

## Scope and prerequisites
The new scope is seven files, including the guide, navigation, publication manifest, and changelog. To validate against master while preserving prerequisite history, this branch includes #4416, #4406, #4399, #4411, #4397, and #4403 and their dependencies. Land prerequisites first, then refresh this branch before merging.

Model/data terms are immutable provenance snapshots, not an allowlist or runtime license gate. No new dependency or weight bundle is added.

## Validation
- Full suite: 26,408 passed, 156 skipped, 11,380 subtests passed.
- 31 focused controls passed on Python 3.12 and 3.11, including all six actual modality fixtures.
- Canonical format, lint, format-check, scoped type checks, and explicit module mypy passed.
- Scoped pre-commit, Bandit, secret scanning, and public API compatibility passed.
- Strict docs/Pages build, routes, feeds, and publication validation passed.
- Exact guide example executed with OS-level network denial.
- Wheel/sdist built offline, Twine passed, and both contain byte-identical module source.
- Incoming attribution policy passed for all 50 commits.

## Documentation and review boundaries
The guide covers protected packet delivery, evaluator-only mappings, caller-governed qualifications, exact adjudication bindings, non-compensable failures, case-level Wilson intervals, and complementary suppression. It also explains limits of blinding, correlated samples, and repeated-release differencing.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `05a64658aab5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.