# Issue

**Title:** Preserve whole-slide tile provenance through aggregation

## Description

## Description
Tile features lose auditability when aggregation drops source coordinates, selection evidence or preprocessing history. This change freshly verifies the original tile plan and requires exactly one matching result for every selected tile before computing a deterministic feature mean. Missing, duplicate, skipped, stale or spatially inconsistent references block the complete result.

## Type of Change
- [x] New feature
- [x] Documentation and focused regression coverage

## Changes Made
- Bind stable tile identities to original slide/level/bounds, plan and mask selection, processed input, provider, feature-space and feature digests.
- Validate crop, resize, quarter-turn and flip chains and preserve exact rational mappings alongside unchanged original visual citations.
- Retain all tile-selection evidence, excluded background candidates, unknown coverage and rounded source-edge gaps.
- Compute protected equal-weight tile means only after complete provenance checks, with value-free audit reports and explicit review-required status.

## Testing
- [x] 24 focused provenance controls; 114 combined tests and 10 subtests.
- [x] Full suite: 24,645 passed, 158 skipped and 11,361 subtests passed.
- [x] Canonical format, lint, format-check, type and brand checks; explicit module mypy.
- [x] Public API compatibility, strict documentation build and executable synthetic guide example.
- [x] Scoped pre-commit, Bandit, secret scanning and complete incoming commit attribution.

## Documentation
- [x] Guide, navigation and publication registry updated.
- [x] Public API docstrings and changelog updated.

## Dependencies and Merge Order
No new third-party dependencies. This branch contains #4390 (tile planning) and #4385 (source evidence), preserving both original commits through a prerequisite merge. Merge both prerequisites before this PR, then refresh from master and revalidate. The tile-provenance implementation is its own final commit; the current master-targeted diff includes prerequisites so the complete CI matrix runs.

The computation is explicitly an equal-weight mean over tiles, including overlapping tiles and different levels. It is not spatial weighting or clinical qualification. Pixel processing, decoder correctness and the truth of upstream processed-input/provider digests remain adapter responsibilities. This Python aggregation layer does not add a model or Swift UI.

## Related Issues

## Example
The executable guide computes a synthetic two-tile mean, preserves the original source box, records unknown selection coverage, omits features from reports and proves arrival-order independence.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fcbd7114a95b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.