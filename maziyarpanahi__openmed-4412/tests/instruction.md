# Issue

**Title:** feat: render synthetic clinical documents with layout truth

## Description

## Description
OCR and document-understanding fixtures need generated content whose word positions remain traceable through scan damage. This renders synthetic clinical forms, letters, labels and fax-like pages, with measured glyph boxes, page reading order, canonical fact/PHI annotations and actual scan effects.

## Type of change
- [x] New feature
- [x] Documentation and test coverage

## Changes
- Generate content from the five existing clinical-note grammars and paginate without silently dropping words. Draw synthetic-copy stamps, repeated identifiers and explicitly untranscribed handwriting placeholders.
- Execute seeded shear, blur, scanner speckles/dropouts, occlusion and JPEG roundtrips; preserve clean glyph masks, transformed geometry, visible support and fully hidden gold annotations.
- Bind clean/final source-linked evidence graphs to actual PNGs. Reproduction rerenders content and pixels and checks font/runtime/specification receipts.
- Keep text and image payloads explicit, reports value-free, fonts local, and work/output sizes bounded. No network calls, file writes or added dependencies.
- Register the public guide in navigation and the publication inventory, and add the changelog entry.

Depends on the fused-evidence implementation in #4385. The branch also carries the previously validated scanner-install and documentation-search accessibility fixes as separate commits.

## Testing
- [x] 61 focused renderer controls pass on Python 3.12 and frozen Python 3.11, including all four layouts and five grammars, real pixel corruption, hidden PHI, pagination, large-font footers, offline reproduction and an executable guide.
- [x] Final full offline suite on `14ea089831f5b1e02371754acb7fd424e9c23d4d`: 25,662 passed, 155 skipped and 11,361 subtests passed in 205 seconds.
- [x] Canonical format, lint, format-check and scoped type checks; explicit module type checking; public API and dependency-license checks.
- [x] Scoped pre-commit hooks, including security and secret checks; workflow and JavaScript syntax checks.
- [x] Complete incoming commit-attribution validation.
- [x] Strict documentation/Pages build, internal routes, feeds and publication metadata passed. Documentation controls passed in Chromium, Firefox and WebKit.
- [x] Wheel and source distribution match final renderer source bytes; Twine validation passed for both.

## Documentation
- [x] Public API docstrings, executable guide, navigation, publication inventory and changelog updated.
- [x] Visibility is documented as geometric support, not OCR readability or clinical qualification. JPEG ringing and contrast changes can extend beyond the masks. Handwriting placeholders have placement truth, not transcriptions.

## Dependencies
- [x] No new package dependencies, bundled fonts, models or datasets. Rendering uses the existing optional Pillow installation and qualified local font helpers.

## Examples
With seed 42 and the encounter grammar, default forms, letters and faxes each render one page with 38 words; the compact label layout renders three pages with 50 words including repeated footer annotations. Representative form, label and corrupted fax rasters were visually inspected locally.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e6578281153b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.