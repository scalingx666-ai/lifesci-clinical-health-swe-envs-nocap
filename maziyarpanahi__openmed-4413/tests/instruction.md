# Issue

**Title:** feat: generate synthetic DICOM overlays and metadata

## Description

## Description
Burned-in identifier and metadata redaction need fixtures whose sensitive regions are known precisely. This generates actual uncompressed Part 10 DICOM files from synthetic grayscale canvases, with matching metadata, pixels, tight glyph masks, privacy boxes and source-bound mask lineage.

## Type of change
- [x] New feature
- [x] Documentation and test coverage

## Changes
- Generate rings, gradient or bounded-noise canvases with five paired metadata/pixel identifiers, field labels, orientation and acquisition annotations, an explicit synthetic disclosure and a pixel ruler.
- Serialize native 8-bit MONOCHROME2 Secondary Capture DICOM with matching dimensions, deterministic UIDs, consistent file metadata and correct odd-length PixelData padding.
- Preserve exact text spans, tight masks, the combined PHI mask, ruler geometry and privacy labels for all eight identifier metadata fields. Bind mask lineage to the actual DICOM bytes.
- Keep raw DICOM, images, identifiers and text in explicit protected test payloads; validate value-free reports and reproduce actual files to reject changed data or receipts.
- Add the public guide, navigation, publication inventory and changelog entry.

Depends on the mask-lineage implementation in #4393, which includes #4385. The branch also carries the established scanner-install and documentation-search accessibility fixes as separate commits.

## Testing
- [x] 37 focused controls cover actual DICOM/PNG roundtrips, generated metadata alignment, tight glyph pixels, omission leakage, ruler/acquisition pixels, odd dimensions, font/runtime reproduction, bounds and an executable guide.
- [x] Related Python 3.12 suite: 132 passed and 25 subtests passed. Frozen Python 3.11 suite: 130 passed, 2 documentation-dependency skips and 25 subtests passed.
- [x] Canonical format, lint, format-check, scoped types, explicit module type checking, public API and dependency-license checks.
- [x] Scoped hooks including security and secrets; workflow/JavaScript syntax and complete incoming commit attribution.
- [x] Frozen Python 3.11 development install and lock validation; all non-root locked package records unchanged.
- [x] Final full offline suite on `1a39dd7087a0442ec782685c169a879389541e4b`: 25,671 passed, 155 skipped and 11,361 subtests passed in 196 seconds.
- [x] Strict Pages build, internal routes, feeds and publication metadata passed. Documentation controls passed in Chromium, Firefox and WebKit.
- [x] Wheel and source distribution match final source bytes; Twine validation passed for both.

## Documentation and limits
- [x] Updated public API docstrings, executable guide, navigation, publication inventory and changelog.
- [x] Documented generated-only input, actual metadata/pixel correspondence, privacy flags, pixel-only ruler units, local fonts, bounded resource use and reproducibility limits.

Fixtures deliberately contain synthetic identifiers and declare `BurnedInAnnotation=YES` and `PatientIdentityRemoved=NO`. They are redaction test inputs, not anonymized clinical images. There are no patient-derived pixels, model downloads, arbitrary source-image inputs, inference or clinical qualification claims.

## Dependencies
- [x] Enable the existing optional pydicom dependency in the development extra so CI exercises real DICOM parsing. No new runtime dependency or bundled font/model/dataset is introduced.

## Example
Seed 42 with the default 640 × 512 ring canvas produces one DICOM image with 14 painted text segments, five PHI masks, eight labelled identifier metadata fields and one pixel ruler. The actual image and combined PHI mask were visually inspected locally. An independent negative control confirms that omitting one identifier mask leaves ink in its protected region.

## Nix development-shell follow-up
The first Nix run reached test collection but failed because its separately maintained development shell lacked `pydicom`. Commit `31390818e` adds that existing dev-extra dependency to `flake.nix`; runtime source and tests are unchanged. The pinned nixpkgs revision supplies pydicom 3.0.2. All 37 focused DICOM tests, repository hooks and the six incoming commits' attribution policy pass. Nix is not installed on the local host, so the corrected head's hosted Nix build and full CI must pass before merge.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f9ea0ae7729d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.