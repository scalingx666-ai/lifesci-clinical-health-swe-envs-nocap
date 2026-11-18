# Issue

**Title:** Gate sustained local inference on thermal and latency budgets

## Description

## Description

Sustained local inference can start within budget and still return a stale result after throttling. This change checks queue age and fresh thermal/memory observations before dispatch, measures execution independently of the provider, and checks again before returning actual VLM or PHI-screened speech output.

## Dependency and merge order

Built from master `29ffa70050cc7729a0051be419a1b090699a5ed1`, with #4392 at `21fb22a5b3d664b68af2b25e44f302e476c881ed` (including #4388) and contributor #4159 at `b9533d4ba3c510bb9faa6131a6e79bf6f6bd142b`. Those prerequisites are preserved in the branch history. Merge #4388, #4392 and #4159 before refreshing and revalidating this PR; the thermal implementation is a separate commit.

The branch also carries the scanner installer repair from #4406: direct download of the same Trivy 0.76.1 release with SHA-256 verification. Vulnerability scans and failure thresholds are unchanged.

## Type of Change

- [x] New feature
- [x] Documentation and tests
- [x] CI reliability fix inherited from #4406

## Changes Made

- Add bounded per-task budgets, fresh host platform observations, pinned local modes and exact capability admission.
- Dispatch actual local VLM adapters in declared order, preserve history across degradation, reject mismatched model/preprocessing pins, and never retry a failed input automatically.
- Measure single-call and rolling p95 latency, enforce queue and total output age, and retain slow-call evidence even when a post-call sensor observation fails.
- Gate existing speech PHI screening without resetting revisions, context or deadlines; withhold late/overheated output and discard pending text on runtime holds.
- Export only aggregate counters and controlled reasons. Add the two local dispatch paths to the existing reviewed effect inventory.

## Testing

- Full suite: **24,682 passed, 158 skipped, 11,361 subtests passed**, 82 warnings; 316.56 seconds.
- **44 thermal controls** cover actual dispatch, explicit fallback, unknown/stale/regressing observations, queue expiry, mid-call resource changes, independently measured latency, bounded history, provider pins, offline replay and speech privacy.
- Relevant runtime, speech-privacy and vision tests passed during iteration; final full run includes the additional sensor-outage regression.
- `make format lint format-check type-check brand-check`: passed.
- Explicit mypy for `openmed/multimodal/runtime/thermal_gate.py`: passed.
- Public API compatibility and executable guide: passed.
- `make docs-build`: passed, including strict MkDocs (192.47 seconds), Pages metadata, LLM feeds and internal route validation.
- Scoped pre-commit, including Bandit and secret scanning: passed.
- Workflow actionlint, frozen Python 3.11 sync and wheel/sdist builds passed; both artifacts contain the runtime module.
- Complete incoming commit-attribution policy checked before push. Hosted checks run on the published head.

## Documentation and scope

Includes the guide, synthetic executable example, public docstrings, navigation/publication classification and Unreleased changelog. Hosts supply fresh platform observations and qualified, already-loaded adapters. The controller can withhold a result after a native call returns; adapters remain responsible for bounded native execution and cancellation. It does not claim hard real-time guarantees or clinical model qualification.

Speech integration gates PHI screening and release, not microphone capture or ASR execution. Apple thermal sensor acquisition and OpenMedKit integration remain tracked in #3836. Modes never automatically upgrade; re-admitting a rejected mode requires explicit host requalification.

## Dependencies

No new packages, weights, datasets or network services. Reuses the local VLM contract, provider capability matrix and speech withholding buffer. The privacy buffer exposes its existing pinned screen digest for runtime admission.

## Checklist

- [x] Scoped implementation and self-review
- [x] Functional and negative controls with synthetic inputs
- [x] Documentation, example and changelog
- [x] Existing privacy, publishing and analytics boundaries preserved

## Related Issues

Depends on #4392 and #4159
Related to #3836

## Example

A preferred local VLM exceeds its measured latency budget: its actual result is withheld, the failed measurement remains in history, and a later input may use the explicitly qualified fallback. A speech screener that overheats mid-call returns no protected text even if its PHI screening completed successfully.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `11e7f7adbb4f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.