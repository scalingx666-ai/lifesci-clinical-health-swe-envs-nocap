# Issue

**Title:** Quarantine inconsistent multipage document groups

## Description

## Description

Mixed patients, duplicated pages, missing continuations and changed layouts can make whole-packet extraction unsafe. This change compares source-bound observations across complete page groups, returns explicit split or quarantine decisions, and preserves the original page coordinates and redaction-mask lineage.

## Dependency and merge order

Builds on #4393, which includes #4385 and current master `29ffa70050cc7729a0051be419a1b090699a5ed1`. This PR targets master so the full CI matrix runs. Merge those dependencies first, then refresh and revalidate this branch. The separate feature commit is `84b2bd00bbbe755745cf352be305a8f3f3fcc62e`.

Also carries the already validated scanner-installation and dynamic docs-search accessibility repairs from #4406. Their existing security and browser gates remain enforced.

## Type of Change

- [x] New feature
- [x] Documentation and tests

## Changes Made

- Capture typed, packet-keyed identity, template-anchor and continuation digests from actual selected OCR spans, retaining source evidence without storing text or keys.
- Bind actual rendered RGB pixels for duplicate detection, independent of container metadata. Different source pages remain distinguishable and duplicate occurrences are never silently dropped.
- Split at explicit patient-ID boundaries, isolate uncertain identities, and compare secondary identity constraints across complete groups so missing intermediate values cannot bridge conflicts.
- Quarantine repeated or incomplete numbering, inconsistent totals, noncontiguous identity fragments, changed or missing anchors, orphan or cross-patient continuation cues, and rejected mask coverage.
- Verify actual bounded PDF page-tree geometry and complete ordered source coverage when using the PDF wrapper. Recompute attached mask lineage and retain original page/node identities during group selection.
- Return validated value-free findings with explicit split reasons. Reassess original observations before exposing a consistent candidate group; caller-edited reports cannot authorize extraction.

## Testing

Reviewed head: `84b2bd00bbbe755745cf352be305a8f3f3fcc62e`.

- **30 focused synthetic packet controls passed**, including mixed patients, group-wide identity conflicts, exact duplicate pixels, numbering gaps/reversals/repeats, layout drift, continuation failures, source/mask tampering, PDF coverage and privacy.
- **131 related evidence, mask, PDF and packet tests plus 34 subtests passed** on Python 3.12 and in the frozen Python 3.11 environment.
- `make format lint format-check type-check`, explicit module mypy, scoped pre-commit, Bandit and secret scanning: passed.
- Executable guide, public API compatibility, dependency-license policy, workflow actionlint and JavaScript syntax: passed.
- Strict `make docs-build`, including Pages metadata, route and feed validation: passed.
- Wheel/source builds, exact packaged module comparison and Twine: passed.
- Complete incoming commit attribution: passed for all five commits.
- Complete offline suite: **25,664 passed, 155 skipped, 11,361 subtests passed**, 79 warnings; 205.73 seconds on the reviewed head.
- Final Chromium, Firefox and WebKit documentation search, keyboard and accessibility controls: **3 passed**.
- Local validation is complete. Hosted checks are pending on the published head.

## Documentation

Public API docstrings, executable synthetic guide, navigation, publication classification and Unreleased changelog included. The guide documents identity normalization and namespaces, HMAC scope, grouping/quarantine reasons, exact-raster duplicate limits, source-coordinate contracts and PDF/mask integration.

## Dependencies and boundaries

No new packages, models, restricted datasets, network calls or file writes. Reuses existing fused evidence, mask lineage and bounded PDF geometry. The caller supplies qualified local OCR/detector spans and faithful rendered RGB pixels; the library does not claim to detect identifiers or independently verify OCR/rendering correctness. Reports establish structural consistency, not patient identity certification, clinical correctness, PHI absence or permission to disclose data. Human review remains explicit.

## Checklist

- [x] Scoped implementation and self-review complete
- [x] Canonical formatting and focused validation passed
- [x] Documentation and changelog updated
- [x] Incoming commit attribution verified
- [x] Full local suite and final browser controls complete
- [ ] Hosted checks pass on the exact head

## Related Issues

Depends on #4393 and #4385

## Example

Two complete one-page documents with different patient-ID digests become two candidate groups with an explicit identity-change boundary. The second group keeps its original page/node/mask references. A missing-ID page cannot bridge them, and a conflicting date-of-birth digest anywhere within a group quarantines that entire group.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7de287c6681a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.