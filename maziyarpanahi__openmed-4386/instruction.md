# Issue

**Title:** feat: maintain stable session-scoped speaker aliases

## Description

## Description

Keep speaker aliases stable when an acoustic-cluster revision changes ordering or explicitly relabels a cluster. Record merge and split lineage without silently rewriting historical transcript references. Identity claims remain outside the registry, and clinical roles require an explicit reviewer attestation bound to the current session and revision.

## Type of Change

- [x] New feature
- [x] Test addition/improvement
- [x] Documentation update

## Changes Made

- Add bounded, atomic revision updates with opaque cluster references and deterministic alias allocation.
- Preserve aliases on relabel; merge onto the earliest parent alias; allocate fresh aliases after an ambiguous split. Merge/split events clear affected role approvals.
- Reject stale or cross-session reviews, reused retired clusters and malformed lineage without exposing values or partially changing state.
- Publish the guide and preserve all existing provider exports while adding the alias API. Update the export-contract test to verify both public surfaces and object identities.

## Testing

Validated head: `e326cfdc1ef340b3f78f81e24c22cc131ea0268c`, from master `29ffa70050cc7729a0051be419a1b090699a5ed1`.

Validation used the existing locked Python 3.12.12 environment with `PYTHONPATH` set to this checkout.

- `python -m pytest tests/unit/multimodal/streaming/speech -q`: 142 passed, including 32 alias controls.
- `python -m pytest tests/ -q -n 10 --durations=10`: 24,588 passed, 158 skipped; 11,361 subtests passed, 82 warnings.
- `make format`, `make lint`, `make format-check`, `make type-check`, explicit mypy on the new module and public API compatibility: passed.
- Strict `make docs-build`, the guide's runnable example, scoped pre-commit hooks, secret scanning and incoming commit attribution: passed.
- Hosted checks are required on this exact head.

## Documentation

- [x] Public docstrings, guide, navigation, publication manifest and Unreleased changelog updated.
- [x] Document acoustic-lineage assumptions, reviewer responsibilities, bounds and session cleanup.

## Dependencies

No new dependencies or models. The registry receives no audio, embeddings, names or identity claims and performs no network/file operations. It does not infer diarization lineage, authenticate reviewers or qualify speaker-recognition accuracy. OpenMedKit parity is tracked separately in #3679.

## Checklist

- [x] Read contribution and maintainer guidance.
- [x] Scoped code and synthetic regression tests reviewed.
- [x] Owner-authored commit passed attribution policy.

## Related Issues

## Example

An explicit relabel retains `speaker_0001`. Splitting that cluster produces new aliases linked to the original and clears its role approval; a stale or cross-session confirmation cannot assign the new speakers a clinical role.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `63b183670be2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.