# Issue

**Title:** feat: mirror multimodal evidence and outcomes in OpenMedKit

## Description

## Description
Mirror the existing multimodal metadata contracts in OpenMedKit so local applications can consume asset manifests, source visual coordinates, transcript lineage, protected clock bounds and provider outcomes without changing their evidence identity.

Python projections consume the existing source contracts. Swift exposes validated typed values and an injected local adapter protocol. Unknown versions/capabilities, malformed rotations, incomplete provenance and invalidated citation bounds fail before consumption.

## Type of Change
- [x] New feature
- [x] Documentation update
- [x] Test addition/improvement

## Changes Made
- Add a bounded versioned wire projection with canonical SHA-256 identity, exact binary64 fields and Int64-safe sample/clock boundaries.
- Preserve original source geometry separately from validated display rotations, and preserve review holds and provider abstention codes.
- Share 26 synthetic valid vectors and 21 rejection vectors between Python and Swift.
- Run Swift CI when the shared fixture changes.

## Testing
- [x] Full offline Python suite: 25,940 passed, 155 skipped; 11,361 subtests passed.
- [x] Focused Python controls: 24 passed on Python 3.12 and 3.11.
- [x] `cd swift/OpenMedKit && swift test --disable-automatic-resolution`: 160 tests, 17 skipped, zero failures.
- [x] Root `swift test --disable-automatic-resolution`: 153 tests, 14 skipped, zero failures.
- [x] Four shared Swift parity tests and the exact Python guide example passed with macOS network access denied. The already built Swift tests used `swift test --disable-sandbox --skip-build --disable-automatic-resolution --filter MultimodalContractParityTests` inside the network-denying sandbox to avoid nested SwiftPM sandboxing.
- [x] `make format lint format-check type-check`, explicit module mypy, `make format-swift lint-swift`, scoped pre-commit including Bandit/secrets, actionlint and public API compatibility.
- [x] Strict documentation/Pages build, offline wheel/sdist build, Twine and exact packaged source-byte checks.
- [x] Complete incoming commit attribution policy: 12 commits checked.

## Documentation
- [x] Public guide, docstrings and changelog updated.
- Example: the same synthetic source packet yields byte-identical canonical JSON and SHA-256 identity in both languages; malformed rotations return `invalid_multimodal_transform`.

## Dependencies and scope
No new package dependencies or bundled model weights. This branch incorporates prerequisite #4405, including its fused evidence, transcript and ECG prerequisites, plus the existing pinned Trivy installer repair. The issue-specific change is commit `30ab04ed0`.

Packets remain protected metadata. Structural validation does not authenticate acquisition or approve disclosure or clinical action. Injected adapters remain responsible for actual execution, cancellation and resource enforcement; a local-only declaration is not a network sandbox. No microphone, model qualification or application UI is introduced.

## Related Issues

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0715491d425b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.