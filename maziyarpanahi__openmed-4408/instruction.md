# Issue

**Title:** Select DICOM series frames with auditable evidence coverage

## Description

## Description

Running every DICOM frame through a local VLM can exceed the device budget, while silently omitted frames can invalidate evidence claims. This change reads actual native DICOM bytes, selects a deterministic bounded set using geometry, acquisition, display signal and pixel diversity, and keeps every supplied frame visible in an auditable selected/unexamined manifest.

## Dependency and merge order

Built from master `29ffa70050cc7729a0051be419a1b090699a5ed1`, preserving contributor #3622 at `63641a2e95c55174e6799a582f9fcf20c56b00e6`. The prerequisite preflight received a focused repair for malformed, truncated, duplicate or exhausted file-meta headers and bounded copying. Merge #3622 first, then refresh and revalidate this branch; the sampler is a separate implementation commit.

Also carries the validated Trivy installer and dynamic docs-search accessibility repairs from #4406. Scan thresholds, axe checks and test gates remain enforced.

## Type of Change

- [x] New feature
- [x] Prerequisite bug fixes
- [x] Documentation and tests

## Changes Made

- Decode bounded native monochrome classic/enhanced DICOM inputs and validate actual patient-space geometry, acquisition discriminators and UID syntax without exposing raw values.
- Require coverage within each compatible acquisition/geometry group before allocating remaining slots to observed pixel diversity. Low-signal and unselected frames remain explicit; unknown acquisitions require opt-in and independent coverage.
- Bind manifests to all source bytes, inspected geometry, display window and sampling policy, with source digests and frame indexes that make opaque references resolvable by reviewers.
- Recompute the complete selection before actual local VLM dispatch; encode fresh metadata-free PNGs and preserve frame-scoped prompts and limits.
- Reject evidence access for unexamined or abstained frames, and withhold the returned bundle on execution failure. Reports contain references, digests, counts and a mandatory sampled-only human-review notice.

## Testing

- Full suite: **25,695 passed, 153 skipped, 11,361 subtests passed**, 76 warnings; 273.41 seconds on the final implementation.
- **37 functional sampler controls** cover classic/enhanced real synthetic DICOM bytes, acquisition isolation, geometry coverage, quality/diversity, source/frame mappings, resource bounds, malformed metadata, actual model inputs, evidence restrictions, stale bindings, privacy and offline execution.
- Prerequisite transfer-syntax repair: 94 focused controls and 177 related checks (51 subtests) passed, including real native file-meta boundaries.
- `make format lint format-check type-check brand-check`, explicit module mypy, public API compatibility and executable guide: passed.
- `make docs-build`: strict MkDocs plus Pages metadata, feeds and route validation passed.
- Final staged docs search, focus, keyboard scrolling and axe checks: passed in Chromium, Firefox and WebKit (3 passed).
- Scoped pre-commit, Bandit, secret scanning, dependency-license policy and workflow actionlint: passed.
- Wheel and source distribution built successfully and both contain the final sampler; wheel metadata includes the existing pydicom dependency in the development extra.
- CI-pinned uv 0.11.28 lock check and frozen Python 3.11 development install: passed. All existing package versions, artifact hashes and unrelated dependency records remain unchanged.
- Fresh Python 3.11 DICOM/preflight/security checks: **166 passed, 11 subtests passed**.
- Twine metadata checks passed for both wheel and source distribution.
- Complete incoming attribution passed for all seven commits. Hosted checks passed on `bef6839be94350f14eef586e7ed5e57e9d26eafd`: 41 successful, 51 skipped, with no pending or failing checks.

## Documentation and scope

Includes an executable synthetic guide, public docstrings, navigation/publication entries and Unreleased changelog. Supports native implicit/explicit little-endian 8/16-bit MONOCHROME1/2 with explicit geometry. Compressed, color and ambiguous inputs fail closed. The display window and signal/diversity thresholds require task qualification; sampling is not clinical coverage, study completeness or de-identification. Pixels may contain burned-in identifiers. Providers remain trusted local code; cooperative bounds are not decoder process isolation.

This issue names Python orchestration files. Native OpenMedKit provider and evidence parity remain separate accepted work.

## Dependencies

No new runtime dependency, model weights, dataset or network service. Reuses existing optional pydicom, NumPy and Pillow plus the local VLM contract. Adds the already locked pydicom dependency to the development extra so hosted tests execute real synthetic DICOM parsing instead of skipping it.

## Checklist

- [x] Scoped implementation and self-review
- [x] Functional, negative, privacy and offline controls
- [x] Documentation, example and changelog
- [x] Contributor history and existing privacy/publishing/analytics boundaries preserved

## Related Issues

Depends on #3622
Related to #2795 and #2801

## Example

Six synthetic slices at two-millimeter spacing produce a manifest covering all six supplied positions within the configured four-millimeter radius. Only the selected frames reach the provider. Every other frame stays explicitly unexamined and cannot be cited through the result's evidence accessor; the output makes no whole-series diagnosis.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `15aac35daba6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.