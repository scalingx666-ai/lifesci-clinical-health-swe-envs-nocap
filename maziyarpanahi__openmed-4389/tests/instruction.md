# Issue

**Title:** feat: gate local visual extraction on measured image quality

## Description

## Description
Measure image quality before local visual extraction and abstain when the input does not meet the caller's task thresholds. Failed assessments return controlled reacquisition or review reasons without accessing provider metadata or running inference.

## Type of Change
- [x] New feature
- [x] Documentation and focused tests

## Changes Made
- Measure source resolution, grayscale exposure/clipping fractions, contrast, Laplacian sharpness and optional foreground contact with an expected blank boundary.
- Verify bounded PNG/JPEG/WebP geometry before decoding, then reject corrupt inputs, mismatched declarations, unsupported modes/animation/transparency and permissive truncated-image settings.
- Add an opt-in wrapper around the existing local provider contract. Whole-image statistics never silently qualify selected regions.
- Keep raw image data and metadata out of reports and decoder diagnostics. Serialize the warning context to restore shared state correctly across concurrent assessments.

## Testing
Validated on base `29ffa70050cc7729a0051be419a1b090699a5ed1`, head `0fa847895616806cd4c840777adb2c4832d5d78c`, in the locked Python 3.12.12 environment.
- [x] 29 focused quality controls passed, including real blur, exposure, crop-boundary contact, decoder bounds, metadata leakage, concurrency and provider suppression.
- [x] Final full suite: 24,585 passed, 158 skipped, 11,361 subtests passed; 71 existing dependency/test warnings.
- [x] `make format`, `make lint`, `make format-check`, `make type-check`; explicit mypy for the new safety package.
- [x] Public API compatibility, strict MkDocs build and executable guide example.
- [x] Import smoke verified that importing the safety package leaves Pillow unloaded.
- [x] Scoped pre-commit including secret scan; incoming commit attribution policy.
- Hosted checks must pass on this exact head.

## Documentation
- [x] Public docstrings, quality-abstention guide, navigation/publication entry and changelog.

## Dependencies
- [x] No new dependencies. Decoding uses the existing optional Pillow dependency from the multimodal extra.

## Code Quality and Checklist
- [x] Self-reviewed bounds, privacy and concurrency behavior.
- [x] Focused commit using repository-owner identity.
- [x] Synthetic fixtures only; no images, weights or restricted assets bundled.
- [x] Existing callers remain compatible.

## Limits
Policies need task-specific qualification; no clinical thresholds are claimed. Boundary contact is a heuristic for expected blank margins and cannot establish complete anatomy, pages or clinical content. Global statistics can miss localized defects. The opt-in helper supports whole-image requests and refuses selected-region requests until a separately provenance-bound crop is assessed. Model output still requires explicit human review. OpenMedKit parity is separately tracked.

## Related Issues

## Example
A synthetically blurred image has lower measured sharpness and is rejected by a policy set between the original and blurred scores. The result includes `insufficient_sharpness`, action `reacquire_image`, and no provider call. Corrupt input returns a controlled review reason without exposing decoder exception text.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `33a04c2e9451`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.