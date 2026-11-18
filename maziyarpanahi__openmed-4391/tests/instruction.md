# Issue

**Title:** Add owned cancellable multimodal runtime sessions

## Description

## Description

Applications can reuse injected local image, PDF and speech providers through one bounded Python session. Rejected assets never reach provider execution, owned inputs close on every path, and cancellation suppresses results committed after the stop request.

## Type of Change

- [x] New feature
- [x] Documentation and tests

## Changes Made

- Add public asset/provider leases, explicit lifecycle states, ordered metadata events and protected results.
- Preflight immutable bounded snapshots, validate actual image/WAV headers, and resolve missing PDF pixel estimates through the bounded geometry reader. Pass execution limits to document adapters for enforcement during decoding.
- Compose the existing VLM and streaming-ASR contracts, with typed abstention, bounded output and stream abort/cleanup on failure.
- Keep cancellation pending until active work and hooks unwind. Close shared owned leases once, preserve borrowed resources, and count cleanup errors without copying exception text.
- Classify the local execution callback in the existing effect inventory; no remote fallback, model downloads or new dependencies.

## Testing

Base: `29ffa70050cc7729a0051be419a1b090699a5ed1`.
Reviewed head: `b04c65e30a64b937ca92fe4c8ee1510b70b991cf`.

- `python -m pytest tests/unit/multimodal/test_runtime_session.py tests/integration/test_multimodal_runtime_session.py -q`: 38 passed.
- `python -m pytest tests/ -q -n 10`: 24,594 passed, 158 skipped; 11,361 subtests passed, 72 warnings.
- `make format lint format-check type-check`: passed.
- `python -m mypy openmed/multimodal/runtime_session.py --follow-imports=silent`: passed.
- `python scripts/release/check_public_api.py`: passed.
- `python -m mkdocs build --strict`, runnable guide example and `make brand-check`: passed.
- Scoped pre-commit hooks, including Bandit and secret scanning: passed.
- `python scripts/release/check_repo_policy.py --commits origin/master HEAD`: passed.
- Hosted checks are pending on the pushed head.

## Documentation

Published runtime guide, public API docstrings, navigation, publication classification and Unreleased changelog included. The guide explains cooperative cancellation, explicit ownership, adapter allocation obligations and protected-output handling. Synthetic tests qualify composition only; they do not qualify a model or clinical workflow. Python scope is explicit; native integration remains separate milestone work.

## Dependencies

No new package dependencies, models or datasets. Existing modality contracts and preflight components are reused.

## Checklist

- [x] Scoped implementation and self-review complete
- [x] Canonical formatting, lint and local tests passed
- [x] Privacy and ownership failure controls included
- [x] Documentation and changelog updated
- [x] Incoming commit attribution verified

## Related Issues

## Example

A synthetic session processes an image, extracts a PDF, pushes a WAV chunk and finalizes speech as events 0–3 while reusing a shared provider. A cancellation race discards late provider output, closes the owned input after the call unwinds, then releases the provider exactly once. Audit JSON contains only controlled metadata.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f8af09d6c1e1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.