# Issue

**Title:** feat: quarantine instruction cues in document regions

## Description

## Description
OCR and visually recognized document text can contain instructions that redirect a model or workflow. Add deterministic region classification and a prompt-data builder that omits complete quarantined regions until an explicit, content-bound policy or reviewer decision permits inclusion.

**Prerequisite: #4385 (fused image-text evidence).** This branch contains the prerequisite and one separate implementation commit. It targets master for the full CI matrix. Merge #4385 first, then refresh and revalidate this PR; the prerequisite diff will disappear once it lands. Latest master `29ffa70050cc7729a0051be419a1b090699a5ed1` is included.

## Type of change
- [x] New feature
- [x] Documentation and focused regression controls

## Changes
- Classify complete English recognition as source content, form instruction, workflow directive or suspicious model-targeted instruction. Missing/incomplete recognition and unsupported languages remain unassessed.
- Reuse the existing local injection scanner and add model-role delimiters, multiline role headings and model-addressed directives. Preserve original source geometry and Unicode cue offsets.
- Detect directives split across regions and propagate quarantine through overlapping source boxes or OCR spans.
- Construct only admitted structured text data, omitting whole held regions. Rescan after exclusions so removing a middle region cannot silently create a new directive.
- Require explicit scoped release decisions bound to the complete current content, source evidence, order and policy. Retain authority and decision evidence in content-free audit output.
- Add a runnable guide, publication/navigation entries and changelog.

This is a lexical, text-only gateway. It does not decode, OCR, redact or admit original images. Released content remains untrusted data. The guide explains English coverage, false positives, unrecognized attacks, upstream recognition responsibility and the separate controls required before sending actual image input.

## Testing
Validated implementation head: `787ebae9ead961cea96477b3de26c9619f80fd2f`.

- 39 focused instruction-screening controls.
- 137 combined screening, fused-evidence, existing injection-guard and publication tests; 28 subtests.
- Full suite: **24,634 passed, 158 skipped, 11,361 subtests passed**.
- Canonical `make format`, `make lint`, `make format-check`, `make type-check`, `make brand-check`.
- Explicit safety-package mypy; public API compatibility.
- Strict MkDocs build and executable guide example.
- Scoped pre-commit, Bandit, secret checks and complete attribution checks against master and the prerequisite.

Controls cover benign form/workflow text, whole-region withholding, Unicode offsets, split directives, overlapping evidence, post-exclusion attacks, exact-content releases, stale approvals, incomplete recognition, unsupported-language review, JSON structural escaping, resource bounds and protected diagnostic output.

## Documentation and dependencies
- [x] Guide, docstrings and changelog updated.
- [x] Self-review complete; focused implementation commit.
- [x] No new dependencies.

## Example
Two OCR regions containing separate fragments of an instruction override are both withheld. A review decision can release explicitly named regions only for the exact current screening digest. The resulting JSON continues to identify every admitted value as untrusted source data.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `01d714edbce6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.