# Issue

**Title:** Preserve clinical labels through morphology and translation

## Description

## Description

Preserve clinical label offsets through rich morphology and guard protected clinical surfaces during local translation. Unsafe or ambiguous cases return review reasons rather than silently producing corrupted training labels. Translation checks compare protected surfaces and cue counts; acceptance is not proof of semantic equivalence or clinical correctness.

## Included pull requests

- #4271 — configurable morphology-aware projection with code-point, grapheme, UTF-8 byte and normalization maps.
- #4272 — local translator guards for terminology, numbers, placeholders and span provenance.

## Issues resolved

## Maintainer changes

- Update both sources from current `master`, retain contributor commits, add Unreleased entries and preserve all documentation registrations.
- Reject oversized unknown placeholders through canonical string lookup instead of unbounded integer parsing.
- No additional cross-PR runtime fixes; the real combined tree is identical to the complete passing rehearsal.

## Validation

- Focused source tests: 100 morphology and 51 translation checks passed; `make format`, `make lint`, `make format-check` passed.
- Complete rehearsal: 23,691 tests passed, 155 skipped, 11,220 subtests passed.
- Strict docs and three Chromium checks passed: asset budgets, exactly one marketing homepage beacon, and no marketing beacon on clinical demos.
- Wheel and sdist built; both changed package modules matched the source bytes. Wheel 7,978,185 bytes within the unchanged 8,633,884-byte limit.
- Exact final SHA `46f143b571e673a2d8b5ccddc6102787a4f76721`: all gates passed again, including 23,691 tests, 155 skips and 11,220 subtests (219.13s). The final wheel is byte-identical to the passing rehearsal.

## Documentation and dependencies

Both guides, navigation, publication classification and changelog are updated. No new dependencies.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `227f02ebadf6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.