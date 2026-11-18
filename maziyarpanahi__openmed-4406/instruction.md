# Issue

**Title:** Redact ECG identifiers across fields and rendered annotations

## Description

## Description

ECG identifiers can remain in structured headers, filenames or printed labels even when waveform samples are safe. This change inventories the supplied record, coordinates text and pixel redaction across fields and pages, and withholds the entire export if coverage, review or residual checks fail. Successful exports preserve the normalized waveform and unflagged clinical text and calibration.

## Dependency and merge order

This branch includes #4387 at `32f7f4729a27941717bfbe5fc632abc1201f5220` and latest master `29ffa70050cc7729a0051be419a1b090699a5ed1`. It targets master so the required checks run. Merge #4387 first, then refresh and revalidate this branch. The ECG annotation implementation is a separate commit; the cumulative diff also contains the lead-layout prerequisite.

## Type of Change

- [x] New feature
- [x] CI reliability fix
- [x] Documentation and tests

## Changes Made

- Inventory actual fields, original lead observations and exhaustive original-pixel page partitions with stable source-bound provenance.
- Combine a qualified local detector with the existing independent structured-identifier safety sweep, then propagate known identifiers across fields and pages without losing original offsets.
- Require complete host review and hold unknown coverage, identifiers on traces, destructive mask overlap, lead-label damage and stale source/provider bindings.
- Rewrite fields, encode fresh metadata-free PNGs, verify decoded pixels and rerun detection on every actual exported field/page before returning any bundle bytes.
- Keep native OCR input/output in memory, bound resource use, clear sensitive backend exception context and provide separate content-free audit reports.

The vulnerability job failed twice before scanning because its installer could not resolve its download redirect. Scanner setup now downloads the same Trivy 0.76.1 release directly from GitHub, verifies a pinned SHA-256, and preserves every scan and failure threshold.

## Testing

Validation used the shared Python 3.12 environment with this repository on `PYTHONPATH`.

- `python -m pytest tests/unit/multimodal/ecg/ -q`: **157 passed**, including 70 annotation privacy controls.
- `python -m pytest tests/ -q -n 10`: **24,658 passed, 158 skipped, 11,361 subtests passed**, 75 warnings; 258.74 seconds on the final implementation.
- `make format lint format-check type-check brand-check`: passed.
- `python -m mypy openmed/multimodal/ecg/annotation_privacy.py --follow-imports=silent`: passed.
- `python scripts/release/check_public_api.py`: passed.
- `make docs-build`: strict MkDocs and Pages publication metadata, LLM feeds and internal routes passed; strict build 187.37 seconds.
- Executable guide example and scoped pre-commit, including Bandit and secret scanning: passed.
- Final review reproduced and fixed propagation of labeled full-width identifiers into unlabelled ordinary/native-digit copies; original-coordinate regression controls pass.
- Complete incoming commit-attribution policy checked against master before push.
- CI follow-up: actionlint, frozen Python 3.11 dependency sync, 35 vulnerability-gate tests (11 subtests), scoped pre-commit official archive SHA-256 verification, and wheel/sdist builds passed.
- Search accessibility follow-up: a newly inserted overflowing search snippet failed keyboard focus with the original script. The repaired script passed the same regression, keyboard scrolling and unchanged axe checks across Chromium, Firefox and WebKit (3 passed). Strict docs build, brand validation and scoped hooks passed.
- Hosted checks run on the pushed PR head; no merge is requested here.

## Documentation

Includes the executable synthetic example, operational guide, public docstrings, matching navigation/publication classification and Unreleased changelog. The host must establish complete native extraction and qualify OCR/detection for its source surfaces. Review digests are attestations, not authenticated approval. Synthetic tests do not establish clinical OCR recall or model qualification. This API does not rewrite native ECG containers or certify anonymous data.

## Dependencies

No new packages, weights, datasets or network services. Reuses the existing ECG waveform/lead-layout contracts, custom recognizer, safety sweep, streaming Tesseract adapter and verified raster writer. Native Tesseract and language data must already be installed when pages are supplied; the host supplies the loaded local detector.

## Checklist

- [x] Scoped implementation and self-review
- [x] Synthetic privacy, negative and residual controls
- [x] Documentation, example and changelog
- [x] No unrelated API or publishing changes

## Related Issues

Depends on #4387

## Example

A name detected only in a patient header is also masked in matching printed text. The encoded PNG is decoded and checked again; a residual name on any later page withholds all pages. Unflagged calibration pixels and the original normalized waveform remain unchanged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4989ebe5e19e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.