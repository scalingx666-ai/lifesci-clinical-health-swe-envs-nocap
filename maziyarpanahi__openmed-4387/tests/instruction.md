# Issue

**Title:** feat: validate ECG lead identity and layout

## Description

## Description

Review ECG lead names, expected sets, display positions and acquisition timing against an independent layout declaration before canonical channel reordering. Report missing, duplicate, mislabeled or misplaced leads and unverified or inconsistent timing without diagnosing the clinical cause.

## Type of Change

- [x] New feature
- [x] Test addition/improvement
- [x] Documentation update

## Changes Made

- Add bounded digital and image-derived lead observations, explicit expected layouts and deterministic value-free review findings.
- Support canonical digital ordering, declared subsets, standard 3-by-4 column timing groups and explicitly repeated rhythm strips.
- Require image-label confirmation and known timing; distinguish missing sampling metadata from inconsistent sample rates/counts and durations.
- Preserve raw labels only in protected input, excluding them and all waveform samples from representations and reports.

## Testing

Validated head: `32f7f4729a27941717bfbe5fc632abc1201f5220`, based on master `29ffa70050cc7729a0051be419a1b090699a5ed1`.

- `.venv/bin/python -m pytest tests/unit/multimodal/ecg/test_lead_layout.py -q`: 32 passed.
- `.venv/bin/python -m pytest tests/ -q -n 10 --durations=10`: 24,588 passed, 158 skipped; 11,361 subtests passed, 81 warnings.
- `make format`, `make lint`, `make format-check`, `make type-check`, explicit mypy on the new module and public API compatibility: passed.
- Strict `make docs-build`, the guide's runnable example, scoped pre-commit hooks including secret scanning, and incoming commit attribution: passed.
- Hosted checks are required on this exact head.

## Documentation

- [x] Public docstrings, guide, navigation, publication manifest and Unreleased changelog updated.
- [x] Document half-open duration conventions, expected layouts, image-review responsibilities and non-diagnostic limits.

## Dependencies

No new dependencies, data downloads or model inference. Uses the existing ECG lead vocabulary and non-diagnostic notice. This validates declared structural evidence; it cannot detect physical electrode swaps from labels alone or establish clinical signal quality.

## Checklist

- [x] Read contribution and maintainer guidance.
- [x] Scoped implementation and synthetic controls reviewed.
- [x] Owner-authored commit passed attribution policy.

## Related Issues

## Example

Two digital channels labeled II/I in declared I/II positions produce order-mismatch findings. A deliberately repeated rhythm strip is accepted only in its declared rhythm slot. Sequential 3-by-4 display columns may have different time windows while the leads within each column must align.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d878113e38e1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.