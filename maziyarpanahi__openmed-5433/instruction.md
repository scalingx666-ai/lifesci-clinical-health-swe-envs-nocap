# Issue

**Title:** Replace the Android MLX-shaped model-store scaffold with format-aware artifact acquisition

## Description

. Depends on #3605.

This adds a format-aware acquisition contract to OpenMedKit Android in `com.openmed.openmedkit.artifact`. `ArtifactRef` carries format, runtime, revision, digest, size and compatibility. `ArtifactAcquisition.acquire(request)` checks it against an `ArtifactBackendCapability` and returns stable `CACHED` / `VERIFIED` / `DOWNLOADED` / `UNSUPPORTED` / `CANCELLED` / `FAILED` results with value-free reason codes.

It wraps the existing `ModelDownloader` and `ModelCache` instead of adding a downloader. The downloader gets a resumable staging path, and `HttpHuggingFaceModelClient` gets HTTP Range resume followed by a full re-hash; a resumed file that fails the re-check is fetched once more from zero. The cache gets identity-keyed artifact directories, read-only promoted payloads and canonical-path containment checks.

Downloading needs `ArtifactNetworkConsent.GRANTED`; the default is `DENIED`. Format and compatibility checks run before any cache or network access. Concurrent callers for one artifact share one in-process transfer, and an interrupted or cancelled transfer keeps its bytes for resume.

The MLX-named `OpenMedModelStore` members are `@Deprecated` with `ReplaceWith` pointing at the new `acquireArtifact` / `cachedArtifact` / `artifactCacheState`, and the scaffold path builder now rejects `.`/`..` and symlink escapes. The migration note is in `docs/android-integration.md`, and `docs/swift-kotlin-parity.md` is updated.

Budget: the release AAR grows from 496,463 to 581,647 bytes. All of the growth is first-party bytecode; there are no new dependencies, and test fixtures use a `java.net.ServerSocket` loopback server, so the #4535 lockfiles need no regeneration. To keep the gate passing, `android/gradle/budgets.properties` raises `aar.maxBytes` from 512 KiB to 608 KiB. Please review that ceiling.

Breaking: the MLX-named `OpenMedModelStore` members and `OpenMedMLXModelCacheState` are deprecated. They still compile, and `downloadMLXModel` still throws for uncached MLX requests. `cachedMLXModelDirectory` now throws `IllegalArgumentException` for a directory that resolves outside the cache root, and the state queries report such a directory as `missing`. To migrate, use `OpenMedModelStore.acquireArtifact(request, cacheDirectory)` or `ArtifactAcquisition` with an ONNX or TFLite `ArtifactRef`.

Not covered:
- Having the `OpenMed` facade's configured backend declare its own capability is #3605; callers pass `ArtifactBackendCapability` explicitly for now.
- No device or emulator instrumentation test. The offline prepared-device case runs as a JVM test with a SecurityManager that denies sockets.
- Single-flight works within one process, not across processes.
- Signed portable bundles resolve as `UNSUPPORTED` until the #3640 verifier lands.
- No real Hugging Face checkpoints were used; the tests use synthetic artifacts.

Validation:
- `cd android && ./gradlew :openmedkit:assembleDebug :openmedkit:verifyAndroidBudgets` with JDK 11: 126 unit tests passed, AAR 581,647 / 622,592 bytes, cold start PASS.
- `:openmedkit:testDebugUnitTest --tests '*ArtifactAcquisitionTest' --tests '*OpenMedModelStoreTest'`, run 6 times: all passed.
- `pytest tests/unit/android tests/unit/test_publish_workflow_version.py tests/unit/onnx/test_android_parity_fixtures.py`: 45 passed.
- `pytest tests/unit -k "docs or publication or mkdocs"`: 152 passed. The strict MkDocs build is left to CI.
- `ruff check .` and `ruff format --check .`: clean.
- `scripts/security/check_effect_paths.py --check`: verified.
- `mypy`: clean.
- `pytest tests/ -m "not slow and not fuzz" --ignore=tests/unit/training/synthetic/test_dicom_overlays.py`: 27,050 passed, 201 skipped, 11,356 subtests passed. The ignored file fails to collect in the shared venv because `pydicom` is missing; that is a known master issue.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d6f140725222`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.