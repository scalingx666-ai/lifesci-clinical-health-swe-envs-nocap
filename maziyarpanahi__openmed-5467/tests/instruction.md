# Issue

**Title:** Make Swift inference cancellation-, background-, and memory-pressure-safe

## Description

.

Adds `OpenMedRuntime`, an actor that owns one on-device text model session through an explicit `idle → loading → ready → busy(n) → draining → released` state machine (admission, a bounded queue, a shared lazy load, leases, drain, idle release and shutdown), with async `analyzeText`, `extractPII` and `deidentify` calls. Each call runs tokenization, windowing, model prediction, merging and serialization behind cooperative `OpenMedInferenceCheckpoint`s. Output from cancelled work is never delivered, and a lease always outlives the session's use. Memory pressure (`OpenMedDispatchMemoryPressureSource`, wrapping `DispatchSource.makeMemoryPressureSource`), background expiration (opt-in `OpenMedUIApplicationBackgroundExecution`; the default `OpenMedNoBackgroundExecution` is a no-op and is what macOS, watchOS and extensions use) and the clock are injectable protocols. A pressure warning or critical signal refuses new work and drains or cancels in-flight work according to `OpenMedRuntimeConfiguration`. The session is released only after its last lease ends, and a later request reacquires it through the local loader with network access disabled. Background expiration cancels in-flight work, suppresses its output and holds admission until the app returns to the foreground. Lifecycle outcomes are value-free `OpenMedRuntimeError` cases with stable reason codes and retry guidance, and `snapshot()` reports only counts, stage names and monotonic cancel latencies. The synchronous `OpenMed` methods keep their signatures and now share one staged core (`OpenMedInferenceCore`, with the redaction helpers moved there unchanged), so both surfaces produce the same bytes. They observe only the calling task's cancellation; that is the documented synchronous boundary, so no blocking bridge was added or needed deprecating. The new "Lifecycle-managed runtime" section of `docs/swift-openmedkit.md` documents all of this.

Breaking: the synchronous `OpenMed.analyzeText`, `extractPII`, `extractPIIChunked` and `deidentify` now throw `OpenMedRuntimeError.cancelled` when called from a cancelled Swift task, where they used to return a result. To migrate, handle that error or call them outside the cancelled task.

Not covered:
- Simulator and device runs across the Apple support matrix, real peak-memory and leak evidence, and latency-to-cancel on real Core ML or MLX checkpoints. The unit tests drive every signal through deterministic fakes, and SwiftPM CLI skips MLX execution.
- Coordination with the verified cache (#3644) and the execution plan (#3641). Neither is on master yet; both plug in through the runtime's loader seam.

Validation:
- `cd swift/OpenMedKit && swift test --filter OpenMedRuntimeTests`: 25 passed, then 60 consecutive reruns with 0 failures.
- `swift test` in `swift/OpenMedKit`: 349 tests, 18 skipped, 0 failures.
- `scripts/format_swift.sh`: changed only files in this diff. `scripts/lint_swift.sh`: clean.
- `swiftc -typecheck` of the new runtime files against the iOS, iOS Simulator, watchOS Simulator, visionOS Simulator and macOS SDKs in Swift 5 and Swift 6 modes: clean. The only Swift 6 diagnostic is pre-existing, in `PostProcessing.swift`.
- `xcodebuild build-for-testing -scheme OpenMedKit-Package -destination 'generic/platform=watchOS Simulator'`: test build succeeded.
- `xcodebuild build -scheme OpenMedKit-Package -destination 'generic/platform=iOS Simulator'`: build succeeded.
- `ruff check .` and `ruff format --check .`: clean. `scripts/security/check_effect_paths.py --check`: verified. `mypy`: no issues.
- `pytest tests/unit -k "docs or publication or mkdocs or swift or publish_workflow"`: 212 passed, 16 skipped.
- `pytest tests/ -m "not slow and not fuzz" --ignore=tests/unit/training/synthetic/test_dicom_overlays.py`: 27921 passed, 271 skipped. The ignored file fails to collect on master because `pydicom` is not installed in the shared venv.
- The strict MkDocs build and the root-package `swift build`/`swift test` were left to CI.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `745610860fcc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.