# Issue

**Title:** feat: add bounded local speaker diarization

## Description

## Description

Add a provider protocol and an optional local CPU implementation for bounded acoustic turns, explicit uncertainty, and session speaker aliases. Unknown and unstable clusters never become confirmed clinical roles or identities.

## Type of Change

- [x] New feature
- [x] Documentation and focused tests

## Changes Made

- Bind mono PCM16LE windows to their exact audio, revision and timeline; limit windows, turns, clusters and response sizes.
- Apply explicit acoustic relabel/merge/split events through the existing alias contract. Keep role review separate and report unknown overlap honestly.
- Run native inference in a disposable process with cancellation, a deadline, sampled RSS monitoring, bounded pipe I/O, suppressed diagnostics and disabled core dumps. Failure returns no partial observations.
- Require caller-supplied local artifacts with byte hashes, revision records and terms snapshots. No weights, downloads, remote license checks or license allowlist are included.
- Handle the native segmentation grid extending past the final sample by intersecting the interval with the input and explicitly marking that turn unstable.
- Preserve batch-local cluster semantics: no guessed cross-window speaker matching.

This branch includes prerequisite #4400, which carries #4386 and #4388, plus the existing checksum-verified Trivy installer repair. The new implementation is commit f88347535; its own scope is 14 files.

## Testing

- [x] `make format`, `make lint`, `make format-check`, `make type-check`, and explicit mypy on all three new modules.
- [x] `python -m pytest tests/ -q -n 10 --tb=short`: **25,686 passed, 161 skipped, 11,361 subtests passed**.
- [x] Frozen Python 3.12 and 3.11 installs with `--extra dev --extra edge-diarization`; **37 focused controls passed on each**, including actual native model loading and failure cases under OS network denial.
- [x] Actual local synthetic-voice smoke under OS network denial: two clusters for sequential voices; two overlapping turns for mixed voices; silence returns insufficient evidence. This is execution qualification, not a speaker-accuracy or clinical-validity claim.
- [x] `make docs-build`, exact synthetic guide example under OS network denial, public API compatibility, scoped pre-commit including Bandit and secret scanning.
- [x] `uv lock --check`, offline wheel/sdist builds, `twine check`, and byte equality of the final source inside both distributions.
- [x] Dependency license inventory/policy; vulnerability audit of all 13 packages in the frozen optional runtime: no known findings.
- [x] Complete incoming commit attribution: all 7 commits passed.

The full suite's six new opt-in integration skips reflect absent model assets in that environment; all six ran successfully in both dedicated native environments.

## Documentation

- [x] Added the local diarization guide, publication/navigation entries and changelog.
- [x] Documented Linux/macOS support, sampled-memory limitations, caller retention responsibilities, and separate model terms.

## Dependencies

The optional `edge-diarization` extra adds Sherpa-ONNX 2.0.1 and its core package, plus existing locked NumPy and psutil. Existing package versions are unchanged; the lock resolver regenerated some conditional dependency markers. Base SDK dependencies are unchanged. Model weights remain separate caller-owned assets.

## Related Issues

.

## Example Output

A synthetic silence window returns `status="insufficient_evidence"` and no turns. Speech observations report sample intervals, opaque aliases, `confidence=null`, `clinical_role=null`, and either observed or unknown overlap.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8354f91d40a5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.