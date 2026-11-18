# Issue

**Title:** Curate native review packets and adjudicated labels

## Description

## Description

Collect bounded native-language review decisions and turn them into adjudicated training/evaluation label revisions with explicit provenance, policy and supersession rules. Unsafe, stale or ambiguous evidence stays unresolved or invalidated.

## Included pull requests

- #4314 — protected reviewer packets, opaque item IDs, private manifest binding and closed decision imports.
- #4294 — explicit adjudication policy, immutable revisions, stale-evidence invalidation and label/audit exports.

## Issues resolved

## Maintainer changes

- Update both source branches from current master, preserve contributor commits and add scoped Unreleased entries.
- Clarify that deterministic public hashes/seeds provide integrity binding rather than secret-key authentication. Synthetic/de-identified status remains a caller declaration, not proof.
- Validate every supplied decision in one acyclic supersession chain, refusing detached cycles that could otherwise hide behind a valid accepted head.
- No additional cross-PR runtime fixes. The real combined tree is identical to the complete passing rehearsal.

## Validation

- 104 focused tests and `make format`, `make lint`, `make format-check` passed.
- Complete rehearsal: 23,795 tests passed, 155 skipped, 11,220 subtests passed (219.16s).
- Strict docs and three Chromium checks passed: asset budgets, one homepage analytics beacon and clinical-page exclusion.
- Wheel/sdist build and both changed package-module byte checks passed. Wheel 8,009,226 bytes within the unchanged 8,633,884-byte budget.
- Exact final SHA `07b23fc4cca054131776ec4a771a37b8d9b6efc2` passed every gate again: 23,795 tests, 155 skips and 11,220 subtests (224.35s). Its wheel is byte-identical to rehearsal.

## Documentation and dependencies

Updated the reviewer-disagreement guide and changelog. No new dependencies. Review packets and stored source references remain protected evaluator artifacts; this does not establish clinical validation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `09b6ac078366`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.