# Issue

**Title:** Bind DICOM display pixels to reproducible provenance

## Description

## Description

DICOM decoding and display transforms can change the pixels behind downstream visual evidence. This change executes a bounded local rendering pipeline, records actual intermediate pixel digests, and requires reproduction from the original source before region evidence can be reused.

## Dependency and merge order

Builds on #4408, which includes the transfer-syntax preflight from #3622 and current master `29ffa70050cc7729a0051be419a1b090699a5ed1`. This PR targets master so the full CI matrix runs. The cumulative diff includes those dependencies; the separate feature commit is `beec1968d9ac37df452c0a10b908a939756d2654`. Merge the dependencies first, then refresh and revalidate this branch.

## Type of Change

- [x] New feature
- [x] Documentation and tests

## Changes Made

- Execute explicit native, RLE or grayscale JPEG decoding, selected-frame extraction, complete rescale-pair resolution, caller-supplied windowing, photometric conversion, clockwise quarter turns, resizing and fresh PNG encoding.
- Bind the original source, frame reference, runtime fingerprint, actual stage outputs and operation parameters in a canonical digest chain, including identity operations.
- Reproduce the complete pipeline before accepting prior provenance or image-region crop bindings. Reject changed sources, forged chains, stale runtime receipts and decoder drift even when the final displayed image is unchanged.
- Connect actual local VLM requests and their VisualEvidence to source/frame/region provenance. Evidence reuse revalidates source pixels and rejects model abstentions.
- Bound source/header/frame/output work, validate compressed-frame expansion or dimensions before decoding, and return fixed rejection messages without source or backend exception contents.

## Testing

Reviewed head: `beec1968d9ac37df452c0a10b908a939756d2654`.

- Focused synthetic provenance tests: 45 passed, including real native/RLE/JPEG decode paths, color layouts, enhanced rescaling, rotations, resizing, forged/stale evidence and privacy controls.
- Related DICOM tests in the frozen Python 3.11 environment: 82 passed.
- `make format lint format-check type-check`, explicit module mypy, scoped pre-commit, Bandit and secret scanning: passed.
- Public API compatibility and dependency license policy: passed.
- Executable guide and strict `make docs-build`, including Pages metadata, routes and feeds: passed.
- Wheel/source builds, exact packaged module comparison and Twine: passed.
- Complete incoming commit attribution: passed for all eight commits.
- Complete offline suite: **25,738 passed, 155 skipped, 11,361 subtests passed**, 44 warnings; 763.80 seconds on the reviewed head.
- Final Chromium, Firefox and WebKit documentation search, keyboard and accessibility controls: **3 passed**.
- Hosted checks are running on the published head; local validation is complete.

## Documentation

Public API docstrings, executable synthetic guide, navigation, publication classification and Unreleased changelog included. The guide distinguishes the explicit window formula from DICOM default LINEAR semantics and documents supported encodings, runtime qualification, resource limits and evidence reuse.

## Dependencies and boundaries

No new dependencies in the feature commit. Uses existing local pydicom, NumPy and Pillow installations; no codec downloads, automatic fallback, network calls, restricted assets or model weights. This is reproducibility evidence, not a diagnostic renderer, PHI redactor, clinical correctness claim or cryptographic signature. Source images and model text remain protected; reports contain whitelisted metadata and digests. The generic renderer selects one explicit frame and does not claim complete series coverage.

## Checklist

- [x] Scoped implementation and self-review complete
- [x] Canonical formatting and focused validation passed
- [x] Documentation and changelog updated
- [x] Incoming commit attribution verified
- [x] Final full local suite and browser controls complete
- [ ] Hosted checks pass on the exact head

## Related Issues

Depends on #4408

## Example

A synthetic DICOM frame is rendered to a fresh RGB PNG, and an `ImageRegion` is bound to the complete transform chain and its actual crop pixels. Reusing that region after changing the source bytes, frame, window or decoded array is rejected. The guide runs this flow entirely in memory.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0f3df92de096`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.