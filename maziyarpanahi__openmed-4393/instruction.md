# Issue

**Title:** Preserve redaction mask coverage through image transforms

## Description

## Description

Cropping, scaling, rotation and intermediate rasterization can move or expand the pixels that need redaction. This change carries protected source regions through declared geometry and rejects the complete result if any protected support loses coverage. Original evidence coordinates remain intact.

## Dependency and merge order

This branch builds on #4385 (fused image-text evidence), which includes latest master `29ffa70050cc7729a0051be419a1b090699a5ed1`. It targets master so the full CI matrix runs. The cumulative diff includes #4385; this feature is the separate commit `c346f4def13d4295073c8d4d4c003f93f32b090d`. Merge #4385 first, then refresh this branch and revalidate before merging.

## Type of Change

- [x] New feature
- [x] Documentation and tests

## Changes Made

- Add explicit source/target coordinate identities, bounded rational affine composition and crop/quarter-turn/scale helpers using existing source evidence and page-rotation semantics.
- Preserve original source regions and OCR spans, with exact composed coordinate maps and conservative output mask support.
- Distinguish coordinate-only composition from actual raster stages. Materialized intermediate pixels and declared filter margins remain protected through later transformations.
- Check complete protected coverage against rectangle unions, including holes and overlaps, rather than only their outer bounds.
- Fail closed on singular transforms, source/space mismatches, partial or complete crop loss, arithmetic exhaustion or excessive coverage work. Rejections contain no partial masks.

## Testing

Dependency head: `9cd40a77cb88439c4b4a988667e6d4523882604f`.
Reviewed head: `c346f4def13d4295073c8d4d4c003f93f32b090d`.

- `python -m pytest tests/unit/multimodal/privacy tests/unit/multimodal/evidence tests/unit/multimodal/test_page_rotation.py -q`: 91 passed and 35 subtests passed, including 33 mask-lineage controls.
- `python -m pytest tests/ -q -n 10`: 24,628 passed, 158 skipped; 11,361 subtests passed, 89 warnings.
- `make format lint format-check type-check brand-check`: passed.
- `python -m mypy openmed/multimodal/privacy --follow-imports=silent`: passed.
- `python scripts/release/check_public_api.py`: passed.
- Strict MkDocs build and executable guide example: passed.
- Scoped pre-commit, Bandit and secret scanning: passed.
- Complete incoming attribution checks against master and the dependency branch: passed.
- Hosted checks are pending on the pushed head.

## Documentation

Published guide, API docstrings, navigation, publication classification and Unreleased changelog included. The guide covers half-open coordinates, rational serialization, raster expansion, sampling margins, union coverage and fail-closed limits. Geometry propagation does not detect PHI, paint redactions, qualify a renderer or authorize disclosure; those obligations remain explicit.

## Dependencies

No new packages, models, datasets, network calls or file access. Reuses source evidence from #4385 and the existing page-rotation contract.

## Checklist

- [x] Scoped implementation and self-review complete
- [x] Local validation and negative controls passed
- [x] Source provenance and privacy-safe reports preserved
- [x] Documentation and changelog updated
- [x] Incoming commit attribution verified

## Related Issues

Depends on #4385

## Example

A protected source rectangle `(30, 20, 40, 30)` becomes `(20, 10, 30, 20)` after a lossless crop starting at `(10, 10)`, while its source evidence stays unchanged. A crop that loses any protected region returns no masks. A rasterized shear followed by its inverse retains the expanded intermediate pixel support even when the composed coordinate map is the identity.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1b25f371eb6e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.