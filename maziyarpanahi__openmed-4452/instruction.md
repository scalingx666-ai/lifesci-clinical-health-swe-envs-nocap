# Issue

**Title:** Publish the frozen v4.0 OpenMedKit support matrix with unsupported combinations

## Description

.

This adds the frozen kit support matrix as data at `openmed/eval/data/kit_support_matrix.json`, next to the tier budgets. `openmed.eval.kit_support_matrix` loads, validates and renders it. The matrix covers all ten surfaces the portable-kit epic (#3604) names. Each cell records the platform and its bounds, a coarse device class, ABI, runtime pin, execution provider, artifact, families, precisions, tier, status and evidence. The 42 unsupported combinations are a separate list, and each one carries a fixed reason code. `scripts/release/check_kit_support_matrix.py` checks the matrix against the repository and keeps the generated block of the new `docs/openmedkit-support-matrix.md` page in sync. The page is added to the mkdocs nav and to `publication.yml`. The issue's "v3.5" wording maps to v4.0, which absorbed that release, so the matrix and page are titled v4.0.

The coherence check reads:
- both `Package.swift` manifests (platform floors, swift-tools version, MLX linkage)
- the Android kit and Flutter Gradle files (minSdk, compileSdk, targetSdk)
- the Flutter podspecs
- the npm and Cargo manifests and `pyproject.toml`
- the families in `docs/export-matrix.md`, so a cell cannot claim an artifact and precision that the export matrix marks unsupported
- the tiers in `openmed.eval.tiers`

It also fails when any kit manifest gains an ONNX Runtime pin that the matrix does not list.

Runtime skew is listed explicitly, and no pin is changed:
- ONNX Runtime: Android `1.25.1`, Flutter Android and Apple `1.20.0`, Flutter Linux and Windows app-supplied with no pin, web `>=1.20.0`, Python `>=1.16`.
- mlx-swift: `0.31.3` in the root package and `0.31.6` in the nested one (#3929).

A cell can be `supported` only if it names an evidence record. `"evidence": "pending"` forces the cell to `experimental`. Validation also rejects device-identifier shapes, UUIDs, local paths, emails, unknown fields and any device class outside the coarse list. Every problem code is value-free.

At freeze, every evidence record is an existing CI lane, so only 5 cells are supported:
- Python reference contract on Linux, macOS and Windows
- Python ONNX Runtime INT8 on Linux x86_64, through the low-resource lane
- Swift MLX on Apple Silicon macOS

Android is P0 but has no supported cell. Its only lane runs on the JVM and never executes ONNX Runtime, so all Android cells stay experimental until #3938 or #3716 adds evidence. React Native, web, document intake, key stores, Flutter, Electron and Tauri are also experimental-only.

Not covered: no real-device (`device-run`) or signed `release-packet` evidence exists yet. Those record kinds are defined for #3716 and #3932 to fill. The browser WebGPU availability cells for WebKit and Gecko are experimental with pending evidence, because no lane exercises them.

Validation: `python -m pytest tests/unit/eval/test_kit_support_matrix.py tests/unit/test_export_matrix.py tests/unit/test_docs_publication.py -q` (84 passed, 2 skipped), `python scripts/release/check_kit_support_matrix.py` (ok: 5 supported, 44 experimental, 42 unsupported), `ruff check .` and `ruff format --check .` (clean), `python scripts/security/check_effect_paths.py --check` (verified), `mypy` (no issues), `python -m pytest tests/ -q -m "not slow and not fuzz" --ignore=tests/unit/training/synthetic/test_dicom_overlays.py` (27044 passed, 224 skipped; the ignored module needs `pydicom`, which the local venv lacks), `python scripts/release/check_repo_policy.py --commits origin/master HEAD` (passed). The strict MkDocs build is left to CI because mkdocs is not installed locally; the docs publication tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b7c0322f1b17`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.