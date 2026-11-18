# Issue

**Title:** feat: preserve transcript span lineage across revisions

## Description

## Description
Track citations through transcript insert, delete, replace, timestamp-shift and finalize operations. Unaffected token identities and span offsets survive edits; changes to cited text or token identity invalidate the citation and withhold its current coordinates.

## Type of Change
- [x] New feature
- [x] Documentation and focused tests

## Changes Made
- Add a bounded, atomic revision ledger for one stable segment, using opaque session, segment, token and span references.
- Reject stale revisions, reused token identities, invalid timing and resource overflows before changing state.
- Keep transcript text and audio outside the ledger. JSON contains only provenance, offsets, relative timing and controlled reasons.
- Document edit-boundary behavior, finalization, caller responsibilities and separately tracked OpenMedKit parity.

## Testing
Validated on base `29ffa70050cc7729a0051be419a1b090699a5ed1`, head `eacb4021a9b1081165ec1086ec77705c7bd51abe`, using the locked Python 3.12.12 environment with PYTHONPATH pointing at this checkout.
- [x] Streaming tests: 143 passed, including 33 new ledger controls.
- [x] Full suite: 24,589 passed, 158 skipped, 11,361 subtests passed; 82 existing dependency/test warnings.
- [x] `make format`, `make lint`, `make format-check`, `make type-check`.
- [x] Explicit mypy for the new transcript package and public API compatibility check.
- [x] Strict MkDocs build and executable guide example.
- [x] Scoped pre-commit, including secret scan, and incoming commit attribution policy.
- Hosted checks must pass on this exact head.

## Documentation
- [x] Public docstrings, transcript revision guide, navigation/publication entry and changelog.

## Dependencies
- [x] No new dependencies; the ledger is stdlib-only.

## Code Quality and Checklist
- [x] Self-reviewed scope and failure behavior.
- [x] Focused commit using repository-owner identity.
- [x] Synthetic fixtures only; no raw clinical data.
- [x] No publishing or existing API changes.

## Limits
The caller must apply identical edits to its protected transcript. The ledger cannot infer text equivalence or acoustic alignment. Finalization seals lineage, not clinical validity. It does not authenticate adapters or provide persistence/recovery guarantees.

## Related Issues

## Example
A citation at character offsets `4..8` moves to `6..10` after a two-character prefix insertion and retains its original token references. Replacing its cited token invalidates it; reinserting similar text does not revive stale evidence.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `582812352cc1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.