# Issue

**Title:** feat: plan bounded whole-slide tiles with auditable coverage

## Description

## Description
Plan whole-slide inference without decoding a gigapixel frame. Native-level tiles retain overlap, explicit source-coordinate transforms, tissue-mask coverage and auditable exclusions, with bounded batches that must fit the caller's declared working-buffer budget.

## Type of Change
- [x] New feature
- [x] Documentation and focused tests

## Changes Made
- Add deterministic multiresolution tiling using explicit rational pyramid scales, clipped terminal tiles and recorded source-edge gaps.
- Filter bounded coarse masks conservatively: unknown or unsampled coverage stays in the plan for review, and excluded background candidates remain auditable.
- Provide an optional deterministic RGB-thumbnail mask heuristic with explicit caller thresholds.
- Reject oversized candidate grids before mask allocation and reject concurrent working buffers above budget before returning a plan.
- Report only coordinates, digests, counts, controlled decisions and declared resource factors. Source slides and pixel persistence remain caller-owned.

## Testing
Validated on base `29ffa70050cc7729a0051be419a1b090699a5ed1`, head `92b9fbbca7a606a68a7a4ea748d6d86003ecc2ab`, using the locked Python 3.12.12 environment with PYTHONPATH pointing at this checkout.
- [x] Vision tests: 190 passed, including 26 new tiling controls.
- [x] Full suite: 24,582 passed, 158 skipped, 11,361 subtests passed; 75 existing dependency/test warnings.
- [x] `make format`, `make lint`, `make format-check`, `make type-check`; explicit mypy for the new pathology package.
- [x] Public API compatibility, strict MkDocs build and executable guide example.
- [x] Scoped pre-commit including secret scan; incoming commit attribution policy.
- Hosted checks must pass on this exact head.

## Documentation
- [x] Public docstrings, whole-slide tiling guide, navigation/publication entry and changelog.

## Dependencies
- [x] No new dependencies; planning and thumbnail classification use the standard library.

## Code Quality and Checklist
- [x] Self-reviewed coordinate rounding, resource admission and uncertain coverage.
- [x] Focused commit using repository-owner identity.
- [x] Synthetic fixtures only; no slide data or restricted assets.
- [x] Existing APIs remain compatible.

## Limits
This is a coordinate and admission planner. Native-region decoding and model execution remain adapter responsibilities. The memory ceiling covers declared working buffers and reserves, not measured process RSS; adapters must account for decoder/model overhead and release buffers between batches. Coarse masks and color thresholds require task-specific qualification and cannot establish clinical tissue completeness. Tile references hash coordinates and source identity, not decoded pixels.

## Related Issues

## Example
The synthetic controls plan a 40,000 × 40,000 source at two native levels without allocating source pixels, retain uncertain mask regions, preserve fractional-scale source coordinates, and reject a buffer plan exceeding its declared budget by one byte.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8a7d68743f39`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.