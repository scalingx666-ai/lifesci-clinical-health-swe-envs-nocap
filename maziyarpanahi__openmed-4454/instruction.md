# Issue

**Title:** Document export toolchains, artifact licenses and redistribution boundaries

## Description

.

Adds `docs/security/export-redistribution.md`, one page that maps every export command in the export and runtime guides (Core ML, ONNX default/Android/OpenVINO/Transformers.js, MLX, Maple MLX and ONNX, GGUF, AWQ, GPTQ, TensorRT) to its toolchain, with versions as pinned in `pyproject.toml`, `uv.lock` and `openmed/onnx/maple_export.py` at the time of writing. It also lists the runtime libraries each OpenMedKit kit (Swift, Android, web, Electron, React Native, Flutter, Tauri) brings into an app, with licenses read from SwiftPM checkouts, Gradle POMs, and the npm, cargo and pub caches; anything that could not be verified locally is marked "To confirm". Further sections cover restricted and vendor components (ML Kit, QNN, TensorRT, llama.cpp, Hub downloads, the Transformers.js CDN WASM default, LGPL libvips via `sharp`) with their default posture and opt-in path, model-license propagation from model card to artifact to bundle, what OpenMed may and may not redistribute, a never-bundle list matching `AGENTS.md`, and the files each runtime loads offline. The page sits in the Project nav next to the license inventory, is registered in `docs/brand/system/publication.yml`, and is linked from the export matrix, the Swift and Android guides, the QNN and WebGPU runtime pages, and the license inventory.

`tests/unit/test_export_redistribution_docs.py` checks, offline, that every `python -m openmed.*` command, `--profile` and export function in the guides has a toolchain row; that every Swift package, Android `implementation` library, JS peer, Flutter and Tauri dependency named in the kit manifests has a row with a license cell; that cited repository paths, modules and doc links exist; and that the never-bundle list matches the repository rules and the page has no private paths or credentials. Each checker has a negative control. No versions are asserted.

The page records two gaps in current behaviour without changing code. The Core ML converter and the Hub publisher stamp `Apache-2.0` whatever the source license. ML Kit ships in the core Android AAR and merges network permissions into the host app until #3928 lands.

Not covered: the strict MkDocs build was left to CI because `mkdocs` is not installed in the shared venv. Licenses for `electron`, `react`, `react-native`, ONNX Runtime 1.20.0 (Flutter), Qualcomm QNN, NVIDIA TensorRT, PyInstaller, onnxruntime-genai 0.12.0 and onnx-ir 0.2.0 are marked "To confirm" because no local manifest for those versions was available.

Validation: `pytest tests/unit/test_export_redistribution_docs.py` (14 passed), `pytest tests/unit/test_docs_publication.py tests/unit/test_export_matrix.py tests/unit/licenses/test_inventory.py tests/unit/test_publish_workflow_version.py tests/unit/test_export_redistribution_docs.py` (88 passed, 2 skipped), `pytest tests/unit -k "docs or publication or mkdocs"` (166 passed, 14 skipped), `ruff check .` and `ruff format --check .` (clean), `scripts/security/check_effect_paths.py --check` (verified), `mypy` (clean), `scripts/licenses/inventory.py` (passed), `pytest tests/ -m "not slow and not fuzz" --ignore=tests/unit/training/synthetic/test_dicom_overlays.py` (27000 passed, 224 skipped, 298 deselected; the ignored module needs `pydicom`, which the shared venv lacks).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b7c0322f1b17`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.