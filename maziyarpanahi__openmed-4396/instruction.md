# Issue

**Title:** feat: require review before handwriting export

## Description

## Description
Handwritten recognition hypotheses must not enter structured output as verified text solely because a recognizer assigns a high score. Add typed unverified candidates and an exact-content reviewer gate before structured export, preserving original visual evidence.

**Prerequisite: #4385 (fused image-text evidence).** This branch contains that prerequisite plus one separate implementation commit. It targets master so the full CI matrix runs. Merge #4385 first, then refresh and revalidate this PR; the prerequisite diff will disappear once it lands. Latest master `29ffa70050cc7729a0051be419a1b090699a5ed1` is included.

## Type of change
- [x] New feature
- [x] Documentation and focused regression controls

## Changes
- Represent handwritten regions with original source boxes, bounded protected alternatives and uncalibrated or unknown confidence. Candidates remain explicitly unverified at every score.
- Require an explicit reviewer selection, corrected transcription, rejection or abstention. Bind each decision to the complete candidate, including all alternatives, confidence, source geometry and recognition provenance.
- Build structured JSON only after freshly validating every candidate/review pair. Missing, stale, unconfirmed or rejected decisions block the entire batch; no partial export is returned.
- Retain visual coordinates and reviewer/decision lineage while keeping protected values out of representations and audit reports.
- Add a runnable guide, navigation/publication entries and changelog.

Review confirms transcription only. This change does not implement a handwriting recognizer, clinical validation, field grounding, automatic dose/date normalization or a Swift review UI. Applications authenticate reviewers and retain approval evidence; digest binding does not authenticate fabricated decisions.

## Testing
Validated implementation head: `ed878c4ba77ad04319698b93fe503d3ba61869c3`.

- 34 focused handwriting controls.
- 125 combined handwriting, fused-evidence and publication tests; 25 subtests.
- Full suite: **24,629 passed, 158 skipped, 11,361 subtests passed**.
- Canonical `make format`, `make lint`, `make format-check`, `make type-check`, `make brand-check`.
- Explicit handwriting-package mypy and public API compatibility.
- Strict MkDocs build and executable guide example.
- Scoped pre-commit, Bandit, secret checks and complete attribution checks against master and the prerequisite.

Controls cover high-confidence non-approval, explicit lower-score selection, correction without interpretation, unknown confidence, rejected/abstained choices, stale text/score/order/source/geometry, mixed-batch withholding, duplicate identities, protected diagnostic output, JSON structural escaping and resource bounds.

## Documentation and dependencies
- [x] Guide, public docstrings and changelog updated.
- [x] Self-review complete; focused implementation commit.
- [x] No new dependencies.

## Example
Two synthetic readings of the same handwritten region have different scores. Export uses the reading explicitly selected by the reviewer, retains the original visual box, and leaves the original candidate unverified. Changing either hypothesis or its source evidence invalidates that review.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d4395df507fa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.