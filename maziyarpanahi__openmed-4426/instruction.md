# Issue

**Title:** feat: bind native Apple audio capture to ambient consent

## Description

## Description
Bind Apple microphone capture to the existing ambient consent state machine. Capture requires both participant consent and OS permission. Pause, withdrawal, participant changes, interruption, route changes and foreground loss stop admission; no permission grant or interruption-end event restarts recording.

The controller owns its session, fences each recording attempt, and clears bounded PCM allocations on success, rejection and shutdown. A reusable local consumer receives borrowed mono samples with original sample offsets and capture epochs, so dropped callbacks remain detectable as gaps.

## Type of Change
- [x] New feature
- [x] Documentation update
- [x] Test addition/improvement

## Changes Made
- Add an injected source/consumer boundary and a native AVAudioEngine source with explicit permission requests.
- Bound native delivery to one pending/borrowed buffer, preserve sample-rate/timestamp binding, and avoid automatic restart or unbounded queues.
- Account separately for session state, delivered-buffer disposal and source shutdown; a cleanup failure prevents restart.
- Document foreground handling, application microphone configuration, host-owned audio-session activation and downstream retention responsibilities.

## Testing
- [x] Fifteen synthetic capture/native PCM controls passed, including actual AVAudioPCMBuffer conversion, stale callbacks, denial, interruption, participant changes, concurrent withdrawal, failed startup, failed consumer and incomplete cleanup.
- [x] Final focused controls passed with macOS network access denied: `sandbox-exec -p '(version 1)(allow default)(deny network*)' swift test --disable-sandbox --disable-automatic-resolution --filter AmbientAudioCaptureTests`.
- [x] Nested `swift test --disable-automatic-resolution`: 180 tests, 17 skipped, zero failures. Final root package run: 173 tests, 14 skipped, zero failures.
- [x] Scoped native compilation against installed iOS 17, watchOS 10 and visionOS 1 simulator targets. Corrected a UIKit notification availability issue on watchOS.
- [x] Full offline Python regression suite: 25,810 passed, 155 skipped, 11,361 subtests.
- [x] `make format-swift lint-swift`, scoped pre-commit, strict documentation/Pages validation, offline Python package build and Twine passed.
- [x] All 14 incoming commits passed attribution policy.

No validation opened a microphone or requested system permission. Physical-device recording qualification remains outside these synthetic controls.

## Documentation
- [x] Public integration guide, docstrings and changelog updated.
- Example: an old recording callback after withdrawal is cleared and never delivered; its buffer remains accounted without claiming successful ASR.

## Dependencies and scope
No new package dependencies, models, recorder UI, remote transport or audio export. The branch incorporates prerequisite #4418 and its ambient privacy prerequisites, including the existing Trivy installer repair. The issue-specific change is commit `1fb9371a7`.

The host supplies microphone usage descriptions/entitlements, foreground state, and audio-session policy. Local consumer callbacks must be short and synchronous; arbitrary blocking code cannot be preempted. Cleanup covers owned mutable buffers and the source shutdown contract, not physical RAM, OS buffers or undisclosed consumer copies.

## Related Issues

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4bc35007309e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.