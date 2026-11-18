# Issue

**Title:** feat: align multimodal evidence clocks with bounded uncertainty

## Description

## Description

Translate actual audio, transcript, ECG and image evidence into a target monotonic clock only when qualified clock bounds, complete calibration coverage and guaranteed overlap permit it. Missing timing, excessive uncertainty, discontinuities and upstream evidence holds return review-required with no translated timestamps.

This branch preserves prerequisite PRs #4385, #4388 and #4404; #4404 includes #4387, #4394 and #4403. Merge those prerequisites first. The clock-alignment-only change is eight files after integration commit `fbc20ac0a334b3b5f3b494a65ed3615e42f82b8d`. The branch includes current master `29ffa70050cc7729a0051be419a1b090699a5ed1`.

## Type of Change

- [x] New feature
- [x] Test addition/improvement
- [x] Documentation update

## Changes Made

- Fit exact rational feasible affine clock families with explicit anchor uncertainty, qualified rate tolerance and uniform nonlinearity bounds; retain all observations and separate discontinuity groups.
- Propagate both clock models and source timing uncertainty through forward/inverse mappings, with outward rounding, no extrapolation and no clipping to fit resource or uncertainty limits.
- Adapt exact audio plan/chunk references, registered finalized transcript citations, original ECG evidence-window members/current waveform and source image geometry with explicit capture timing.
- Preserve source/candidate holds, verify source snapshots and require guaranteed overlap; identical clock/epoch declarations support direct comparison without claiming wall time.
- Keep payloads and timestamps out of operational reports and errors; bind policies, calibrations and source references through digests.

## Testing

- [x] Added focused synthetic controls for independent affine truth, drift/noisy anchors, large monotonic origins, breaks, uncertain overlap and actual modality reference changes.
- [x] New and existing unit tests pass locally.
- [x] Tested different source types, fractional sample grids and invalid declarations.

Validation:

- Focused clock alignment suite: **73 passed**.
- Full repository suite: **24,910 passed, 158 skipped; 11,361 subtests passed, 74 warnings**.
- Canonical format/lint/format-check/type/brand gates and explicit mypy on the provenance package: passed.
- Public API compatibility and scoped pre-commit hooks, including Bandit and secret scanning: passed.
- `make docs-build`: passed strict MkDocs, publication metadata, LLM feeds and internal-route validation. Executed the guide example successfully.
- Complete incoming commit attribution: passed for all nine incoming commits and the feature commit independently.
- Hosted checks must pass on the exact PR head before merge.

## Documentation

- [x] Added public API docstrings and an executable guide.
- [x] Updated navigation, publication manifest and Unreleased changelog.
- [x] Documented model qualification, full-width uncertainty policy, source timing, reset epochs, protected output and non-clinical limits.

## Code Quality

- [x] Ran the canonical formatting, linting and validation commands.
- [x] Reviewed the implementation and kept changes scoped to the issue.
- [x] Documented exact arithmetic and the conservative uncertainty decisions.

## Dependencies

No new dependencies or network calls. Uses standard-library rational arithmetic and existing source contracts. No model weights, datasets or restricted assets are bundled. Python scope; OpenMedKit integration is tracked in #3679.

A feasible clock fit depends on independently qualified host assumptions; it cannot prove undisclosed drift, timing accuracy or authentic acquisition. Alignment establishes temporal overlap for human review, not clinical agreement or approval. ECG bundles must come from the actual builder or source-verified restoration.

## Checklist

- [x] Read contribution and maintainer guidance.
- [x] Preserved prerequisite implementation commits.
- [x] Used the owner identity and checked complete incoming attribution.

## Related Issues

Related to #2796, #2814, #2810, #2806, #2812 and #3005.

## Example

A synthetic audio window at source-clock 2–3 seconds maps to target-clock 3–4 seconds under a declared one-second offset. A declared pause, missing image timing or uncertain-only overlap instead returns review-required and withholds all translated coordinates. No audio decoding, pixel loading or clinical action occurs.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `da9d11cf460a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.