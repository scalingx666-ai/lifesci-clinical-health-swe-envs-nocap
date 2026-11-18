# Issue

**Title:** Gate pixel exports on complete regional privacy coverage

## Description

## Description

. Image export now has an opt-in gate that executes actual regional detection, requires every decoded frame and carrier to be inspected, resolves critical regions against the proposed masks, and withholds the entire output bundle if any check fails.

The gate returns fresh PNGs only. It never certifies or releases the original image/DICOM container. It inventories native DICOM frames, icons and explicit overlay planes separately, including overlay pixels outside the main image. VLM sampling is recorded but never grants privacy coverage to skipped frames.

## Type of change

- [x] New feature
- [x] Documentation and focused synthetic regression coverage

## Changes

- Source-bound frame plans, complete rectangle-union inspection, explicit ignored-region holds, and critical-mask resolution.
- Actual crop, quarter-turn and nearest-neighbor transforms verified through the existing mask lineage implementation; encoded pixel verification and a required full-output residual detector.
- Deterministic value-free evidence, bounded in-memory processing, cancellation, controlled errors and parser diagnostic suppression. Any failure returns no partial output.
- Public exports, an executable guide, navigation/publication entries and changelog.

## Validation

- 41 focused controls passed, including coverage holes, borders, transforms, stale sources, missing frames, ignored regions, residual findings, metadata exclusion, DICOM icons/overlays, sampling and resource limits.
- 150 related privacy/evidence/DICOM controls passed in the frozen Python 3.11 development environment.
- Canonical format, lint, format-check and scoped type checks passed; the new module also passed explicit mypy.
- Strict docs/Pages build and metadata, route and feed validation passed. The staged search, keyboard and accessibility regression passed in Chromium, Firefox and WebKit.
- Executable guide, public API compatibility, dependency-license policy, scoped pre-commit, Bandit and secret checks passed.
- Complete incoming commit attribution passed for all 11 commits.
- All current hosted checks passed on `df8d3fc097cda4c5c605540346995b68ae76e0ea`, including Nix and the required commit-attribution policy. The earlier canceled attribution run is superseded by the successful current run.

- Wheel and source distribution built with the pinned uv version, contain the exact implementation bytes, and passed Twine.

- Full offline suite on the final commit: **25,806 passed, 155 skipped, 11,361 subtests passed**. Local socket/IPC tests ran with the necessary process access; network-dependent model tests remain separate.

## Dependencies and limits

No new dependencies. The decoder path uses existing Pillow, NumPy and pydicom installations. Local detectors must be qualified for the modality, languages and crop/window configuration; their registration is not a sandbox or a recall guarantee. Unsupported DICOM encodings/carriers fail closed. This is not clinical or compliance certification.

Depends on #4408 and #4393, with prerequisite history preserved. Merge those prerequisites first, then refresh and retest this PR against master.

## Example

The executable synthetic-marker guide returns `accepted=True` and one verified PNG. Missing frame coverage, an uncovered identifier or a residual detection returns `accepted=False` and `outputs=()` for the entire bundle.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c8dc6e87f004`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.