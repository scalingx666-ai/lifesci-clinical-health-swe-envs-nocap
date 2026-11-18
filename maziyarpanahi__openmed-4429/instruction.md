# Issue

**Title:** Gate local OpenMedKit inference on Apple thermal state and latency

## Description

An already loaded local vision model can now refuse queued work when an Apple device is hot and withhold a result if conditions worsen during generation. A critical thermal notification invalidates an in-flight result even when the device cools before the model returns.

- Observe `ProcessInfo.thermalState` and its change notifications; reduce cadence in fair conditions, restrict timed windows in serious conditions, and pause when critical or unavailable.
- Enforce queue age, rolling latency and result age on one monotonic clock. Recovery requires sustained lower pressure. Evidence contains counts, timings and controlled reasons; no prompts, images or generated text.
- Integrate with OpenMedKit's local vision-language generation and document the injectable session. No new dependencies or model downloads.

. Based on the Python reason vocabulary in #4407. The six files in `ed96a5f06` are the changes specific to this issue.

Validation: `make format-swift lint-swift`; nine focused admission tests with network access denied; `swift test --disable-automatic-resolution` in both package roots (165 tests / 17 skipped and 157 / 14 skipped, zero failures); typechecked the thermal controller for iOS, watchOS and visionOS simulators. The offline Python suite passed (25,688 passed, 155 skipped). `make docs-build`, wheel/sdist build, Twine, scoped pre-commit, committed-history secret scan and attribution all passed. Injected thermal transitions exercise the policy; these results do not measure device heat or qualify model performance.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aa465f634447`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.