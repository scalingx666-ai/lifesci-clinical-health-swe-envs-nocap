# Issue

**Title:** Pin the web package's default model revision and add an offline-only mode

## Description

.

The default `extractPii()`/`deidentify()` path now asks the loader for `DEFAULT_MODEL_REVISION` (`79f7db205869b1be4be23ac4f42aa95bdedc5aee`, the current Hub head of `DEFAULT_MODEL_ID`, and the same commit `openmed/eval/arm_latency.py` already pins) instead of the mutable `main` branch. Built-in and custom loaders both receive it. A new `js/openmedkit-web/src/offline.ts` adds `setOfflineOnly()`/`isOfflineOnly()` and a typed `OpenMedOfflineError` with fixed messages and no `cause`. When the package setting is on, or a call passes `offlineOnly: true`, `extractPii`/`deidentify` and `loadOnnxModel`/`loadTokenClassificationPipeline` (`model-loader.ts`) refuse Hub IDs and URLs before any loader, runtime import or fetch runs. These loads then use `allowRemoteModels: false` and `local_files_only`. They also refuse a remote ONNX Runtime `wasmPaths`, such as the jsDelivr default Transformers.js sets in browsers, unless the new `wasmPaths` option supplies a local one, and refuse a remote `env.localModelPath`. Local load failures become `local_assets_unavailable`. The ONNX Runtime Web loader and the WebGPU session were already local-only; in offline mode their load failures map to the same error. Explicit local model paths now always load local-only. The change also hardens offline asset path validation against non-canonical prefixes. The package README covers the pinned revision, offline-only mode, preparing a local copy, and deprecating implicit default-model downloads.

Expected rebase order: #3980, then #4156, then #4249, then this PR. A pairwise `git merge-tree` against each of those heads merges every file this PR touches cleanly. The only conflict is each PR's own `CHANGELOG.md` entry against current master. #4547 conflicts only in the public-API snapshot list.

Breaking: the default model now loads a fixed revision (to track the branch, pass `loaderOptions: { revision: "main" }`). Explicit local model paths ignore `localFilesOnly: false`/`allowRemoteModels: true`, and local-looking references that name another host are refused (pass a Hub ID to load remotely). Asset paths outside Windows drive paths may no longer contain backslashes or control characters (use forward slashes).

Not covered: no real browser run with Transformers.js or ONNX Runtime Web. All loads go through fake runtimes. The jsDelivr `wasmPaths` default and the `env.backends.onnx.wasm` layout were checked against the Transformers.js 4.2.0 source, not observed in a browser. The worker facade (#4547) and the Electron utility process get no new wiring beyond what the shared loaders enforce.

Validation: `cd js/openmedkit-web && npm ci && npm test` (build, typecheck, 40/40 node tests), `npx tsc --noEmit --noUnusedLocals --noUnusedParameters -p js/openmedkit-web/tsconfig.json` (clean), `cd js/openmedkit-electron && npm ci && npm test` (8/8, compiles against the web package source), `ruff check .` and `ruff format --check .` (clean, no Python changes), `python scripts/security/check_effect_paths.py --check` (verified), `mypy` (clean), `python -m pytest tests/ -q -m "not slow and not fuzz" --ignore=tests/unit/training/synthetic/test_dicom_overlays.py` (27286 passed, 232 skipped, 298 deselected; the ignored module fails to collect on master because `pydicom` is missing from the shared environment), `python scripts/release/check_repo_policy.py --commits origin/master HEAD` (passed). Mutation checks: removing the revision pin, the Hub-ID refusal, the WASM-path refusal or the fail-closed wrapper each makes the new tests fail.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f698a58f9e7f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.