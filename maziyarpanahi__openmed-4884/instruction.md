# Issue

**Title:** Run exported token-classification ONNX graphs on WebGPU and WASM in a browser lane

## Description

.

This adds a browser lane that runs complete exported token-classification graphs on ONNX Runtime Web. `openmed/onnx/browser_lane.py` builds a tiny randomly initialised BERT classifier offline (seed 3940) and exports fp32 `model.onnx` and fp16 `model.webgpu.onnx` with `openmed.onnx.convert.convert`. It also derives a negative-control graph with an appended `Mod` (an op with no WebGPU kernel) and writes synthetic feeds plus Python ONNX Runtime reference logits. `tests/browser/ort-lane` serves these files, ONNX Runtime Web 1.31.1 from the local npm package and the built `openmedkit-web` runtime from one loopback origin (COOP/COEP for threads). It runs each case through `loadWebGpuTokenClassificationSession()` on `webgpu`, threaded `wasm` and single-thread `wasm`, aborts and counts every cross-origin request, and writes one value-free record per case: provider, browser version, browser-computed digests, tolerances, and outcomes including fallback op types and node placement. `python -m openmed.onnx.browser_lane check` validates and gates the records. A separate `ort-browser-lane` job in the Pages workflow and `make ort-browser-lane` run the lane, and `docs/runtimes/webgpu.md` documents it.

The lane exposed an exporter bug: ONNX Runtime could not load the fp32 `model.onnx` from disk. Python ORT 1.23.2 and 1.31.1 and ORT Web 1.31.1 all failed with `[ShapeInferenceError] Cannot parse data from external tensors`, because `_consolidate_external_onnx_data` moved every initializer into `model.onnx.data`, including the Slice constants that shape inference reads. It now keeps tensors smaller than 1 KiB inline (the ONNX default threshold) and writes no sidecar when no tensor is large. A regression test loads a consolidated Slice graph in ONNX Runtime; it fails with the old threshold.

Observed: on Chrome 156 with Apple Metal all five cases pass. Threaded WASM (4 threads, isolated) and single-thread WASM (not isolated) are within 2.1e-6 of the Python reference (tolerance 1e-4), WebGPU fp32 within 2.9e-6 (tolerance 1e-3), and WebGPU fp16 within 1.7e-2 (tolerance 5e-2). Every case decodes identical spans. With ORT Web 1.31.1 every exported BERT graph is `partial`: its int64 shape subgraph, `IsNaN` and `Max` (38 nodes) run on the WASM CPU provider. The control adds `Mod` and is reported `partial`, as required. Playwright Chromium 151 in the pinned Playwright container (SwiftShader) gives the same results, except for fp16 (below).

Not covered: SwiftShader has no `shader-f16`. In CI the fp16 WebGPU case is therefore recorded as `unavailable` (`webgpu_shader_f16_unavailable`); the job accepts only that reason, and every other case must pass. fp16 WebGPU parity is verified only on the local Metal GPU. Release checkpoints (#3716), Firefox, WebKit and a support-matrix consumer of the records are out of scope.

Dependencies: `onnxruntime-web` 1.31.1 (MIT) and `@playwright/test` 1.62.0 (Apache-2.0, already pinned by the brand suite) are dev dependencies of the private `tests/browser/ort-lane` package only; `npm audit` reports 0 vulnerabilities. The CI job installs the existing locked `onnx` extra.

Validation:
- `pytest tests/unit/onnx/test_browser_lane.py tests/unit/onnx/test_onnx_convert.py tests/integration/test_ort_browser_lane.py -q`: 79 passed in a venv synced from `uv.lock` with the `onnx` extra; 69 passed and 7 skipped (no onnx) in the shared dev venv.
- `OPENMED_ORT_LANE_CHANNEL=chrome npm --prefix tests/browser/ort-lane test`: 8 passed (macOS, Metal).
- The same suite in `mcr.microsoft.com/playwright:v1.62.0-noble@sha256:02bbb2…` with `OPENMED_ORT_LANE_ALLOW_UNAVAILABLE=webgpu_shader_f16_unavailable`: 8 passed (linux/amd64 image, run under emulation on an arm64 Mac).
- `python -m openmed.onnx.browser_lane check`: passes on the Metal records. On the container records it fails without the flag and passes with `--allow-unavailable webgpu_shader_f16_unavailable`.
- `ruff check .` and `ruff format --check .` (clean), `check_effect_paths.py --check` (verified), `mypy` (clean), `pre-commit run --files <changed>` (passed), `tsc --noEmit --strict` on the spec and config (clean), `check_github_actions_refs.py --require-sha` (passed).
- `pytest tests/ -q -m "not slow and not fuzz" --ignore=tests/unit/training/synthetic/test_dicom_overlays.py`: 27043 passed, 229 skipped, 298 deselected. `test_dicom_overlays.py` is ignored because `pydicom` is not installed in the shared venv (same on master).
- The strict MkDocs build is left to CI.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `201f570abb25`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.