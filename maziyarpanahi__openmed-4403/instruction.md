# Issue

**Title:** Extract reviewable ECG timing candidates from quality-gated signals

## Description

## Description

Derive review-only rate, PR, QRS and uncorrected QT candidates from freshly quality-gated ECG samples. Keep original lead/sample fiducials and withhold measurements when boundaries, beat assignments or leads disagree.

This is a conservative baseline-excursion detector with explicit caller-qualified settings, not a clinically qualified general-purpose delineator. Synthetic tests establish software behavior, not clinical accuracy. No diagnosis, treatment recommendations, QT correction or automatic clinical action.

## Type of change

- [x] New feature
- [x] Documentation and meaningful synthetic regression tests

## Changes

- Reassess original acquisition quality and reviewer confirmation; measure only independently required leads.
- Extract actual ventricular and P/T excursions, with baseline guards, two-threshold boundary sensitivity and bounded sample-domain searches.
- Preserve original source-relative offsets, per-lead fiducials, acquisition context and complete algorithm/policy/result provenance.
- Abstain on missing or competing waves, reused T/P assignments, inconsistent beat counts, peak alignment or measurement spread. Never interpolate missing samples/beats or select a favorable lead subset.
- Keep measurements protected in memory; provide deterministic value-free audit JSON. Agreement scores are explicitly not calibrated probabilities or clinical error bounds.

## Prerequisites and merge order

Contains the preserved prerequisite commits from #4387 (lead layout) and #4394 (signal quality), based on current master `29ffa70050cc7729a0051be419a1b090699a5ed1`. Merge #4387, then #4394, then this PR. The issue-specific change is commit `9f137b5d95cf442aa32ff4e8f166faa135202205`: six files and 1,295 added lines. Targeting master keeps the normal hosted validation active.

## Validation

- Focused interval tests: 55 passed.
- Full suite: 24,708 passed, 158 skipped; 11,361 subtests passed (80 warnings).
- Canonical `make format`, `make lint`, `make format-check`, `make type-check`, `make brand-check`: passed.
- Explicit module mypy, public API compatibility, effect-path inventory and runnable guide: passed.
- Strict MkDocs and complete `make docs-build`, including publication metadata and internal routes: passed.
- Scoped pre-commit, Bandit and secret scanning: passed.
- Complete incoming attribution: three commits against master; one feature commit against the prerequisite head. Owner identity preserved.
- Hosted checks will run on this exact pushed head.

## Documentation and dependencies

Guide, API docstrings, navigation/publication registration and Unreleased changelog included. No new dependencies, downloaded datasets, external services or bundled detector code. This issue scopes the implementation to Python.

## Related issue

## Example behavior

Synthetic two-lead pulses produce bounded timing candidates and original-grid evidence. Removing the observed P wave withholds PR while preserving independently supported rate/QRS/QT candidates; assigning the same excursion as T and the next P withholds both dependent measurements.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cbcfd3ec8e31`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.