# Issue

**Title:** Attach ECG candidates to waveform evidence windows

## Description

## Description

Attach ECG timing candidates to the original lead samples, observed fiducial brackets, acquisition quality and transform provenance needed for human review. Rate evidence includes both consecutive ventricular complexes; PR and QT retain their observed wave endpoints.

Saved metadata is restored only after rerunning acquisition quality and actual timing extraction against the original local waveform. Altering offsets, fiducials, policies, source identity or abstentions is rejected even if the saved hashes are recalculated.

## Type of change

- [x] New feature
- [x] Documentation and synthetic regression tests

## Changes

- Build complete per-lead sample windows from fresh candidates, retaining original sample indices, lead-local beat identities and source-relative timing.
- Refuse incomplete padding and resource overflow instead of clipping or dropping evidence.
- Preserve aggregate abstention when only some lead windows exist; never fabricate missing P/T boundaries or clinical approval.
- Bind ordered upstream transform declarations, actual detector centering, original normalized sample slicing, policies and quality context.
- Serialize protected timing descriptors without samples or measurement values; provide a separate counts/digests audit report.
- Restore with bounded, typed metadata validation and fresh source evidence. Reject duplicate keys, nonfinite numbers, missing/extra windows and stale or altered records.
- Expose original samples only through exact window membership, a current full-waveform fingerprint and explicit local-viewer confirmation.

## Prerequisites and merge order

Contains preserved prerequisite commits from #4387, #4394 and #4403. Merge them in that order before this PR. Targets current master `29ffa70050cc7729a0051be419a1b090699a5ed1` so the normal hosted checks run.

The issue-specific commit is `c3597c4f975a4f986ea014bc51c40e42c64a7795`: six files, 1,178 added lines.

## Validation

- Focused evidence-window tests: 57 passed.
- Full suite: 24,765 passed, 158 skipped; 11,361 subtests passed (81 warnings).
- Canonical `make format`, `make lint`, `make format-check`, `make type-check`, `make brand-check`: passed.
- Explicit module mypy, public API compatibility, effect-path inventory and linked runnable guide example: passed.
- Complete `make docs-build`, including strict MkDocs, publication metadata, LLM feeds and internal routes: passed.
- Scoped pre-commit, Bandit and secret scanning: passed.
- Incoming attribution: all four commits against master and the one feature commit against its prerequisite head passed.
- Hosted checks will run on this exact pushed head.

## Documentation and dependencies

Guide, API docstrings, navigation/publication registration and Unreleased changelog included. No new dependencies, network calls, signal files or bundled datasets. This Python layer retains the detector's non-diagnostic limitations; it does not authenticate source declarations, approve clinical evidence or label real ECG data synthetic.

## Related issue

## Example behavior

A serialized rate window restores with the same two beat references and exact original lead slice. Changing a fiducial or source offset fails replay. When one lead lacks a P wave, the other lead's PR evidence remains available for inspection while the aggregate PR measurement stays abstained.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `63f47e8f4e19`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.