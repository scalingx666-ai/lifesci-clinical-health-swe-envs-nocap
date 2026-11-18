# Issue

**Title:** fix: block promotion when the challenger omits a critical axis

## Description

## Description
`_build_ledger` dropped a critical-label recall the challenger did not report, and compared only the gates present in both reports. A challenger that left an axis out therefore produced no entry for it, and `_decide` had nothing to block on. This makes a missing safety axis a blocking regression instead of a silent skip.

## Type of Change
- [x] Bug fix (non-breaking change which fixes an issue)

## Changes Made
- `GateLedgerEntry` gains an optional `reason` field, serialized in `to_dict()` only when set, so records written before this change stay byte-identical.
- New `_missing_entry()` helper: a blocking `REGRESSION` entry for an axis the champion reports and the challenger does not, tagged `missing_in_challenger`.
- `_build_ledger`: a critical label in the champion's report but not the challenger's now produces that entry; so does a gate the champion **passed** that the challenger omits. An axis the champion itself never reported still produces no entry, and a gate the champion already failed is not a regression when dropped.
- `_decide` names the reason in the reject text: `blocking safety regression on per_label_recall.API_KEY (missing_in_challenger): …`.

## Testing
```
.venv/Scripts/python.exe -m pytest tests/unit/eval/test_champion_challenger.py -q
23 passed, 4 subtests passed in 5.90s
```

Four tests added, all synthetic and offline:
- `test_challenger_missing_a_critical_label_recall_blocks` — REJECT, entry tagged `missing_in_challenger`, the label named in `verdict.reasons`.
- `test_challenger_missing_a_gate_the_champion_passed_blocks` — same for `gate.G3`.
- `test_champion_missing_the_axis_stays_unaligned` — negative control: no entry when the champion never reported it.
- `test_challenger_missing_a_gate_the_champion_failed_does_not_block` — negative control: dropping a gate the champion failed is not a regression.

Checked the tests bite: with the production change stashed, three of the four fail (`'GateLedgerEntry' object has no attribute 'reason'`); all four pass with it restored.

## Documentation
- [x] I have added docstrings to new functions/classes
- [ ] CHANGELOG.md untouched — say the word if this repo wants a release note for a P2 fix.

## Code Quality
- [x] `ruff check` clean on both changed files
- [x] `scripts/release/check_repo_policy.py --commits upstream/master HEAD` → `Commit attribution policy passed: 1 commits checked`
- [x] Self-review done

## Dependencies
- [x] I have not added any new dependencies

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ef71c5b0688a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.