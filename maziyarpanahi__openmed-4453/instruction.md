# Issue

**Title:** Publish the OpenMedKit portable-kit threat model

## Description

.

This adds `docs/security/openmedkit-threat-model.md`, the threat model for the portable OpenMedKit runtimes. The issue was written for v3.5, which has since been folded into v4.0, so the page models the v4.0 kits: Swift OpenMedKit and its share and action extensions, Android OpenMedKit, `js/openmedkit-web`, React Native, Flutter, Electron and Tauri.

The page covers assets, seven trust boundaries, data flows (model acquisition, cache, inference, share and export, logs and diagnostics) and seven adversaries. It then lists 29 abuse cases, among them tampered or downgraded bundles, manifest path escape, cache poisoning, implicit tokenizer network access, cloud fallback, WebGPU and worker isolation, Electron IPC and Tauri sidecar abuse, React Native and Flutter bridge misuse, PHI in errors, logs and containers, weak hash keys, key-store misuse, offset-unit confusion and supply chain. Each case maps to a source path or test on master, or to the open v4.0 issue that owns the control (#3640, #3644, #3930, #3942, #3943, #3714, #3715, #3718, #3710, #3937, #3951 and others), and states the risk that remains.

The page also lists controls that no issue owns yet, residual risks, unsupported deployments and out-of-scope threats. Clinical-brief generation stays with #3233. Gaps found while reviewing master are described only at the threat-class level, with no reproduction steps.

The page is in the security nav and in `docs/brand/system/publication.yml`. It is linked from the Swift, Android and ONNX Runtime Web guides and from the redactor threat model.

The new `tests/unit/test_openmedkit_threat_model_docs.py` checks that:
- every repository path quoted on the page exists, and every short file name also appears as a full path;
- every surface and trust boundary has at least one abuse case;
- every row names a control path or an owning issue, plus a residual risk;
- owners and the owning-issue table match both ways;
- the page has a nav entry and is registered in `publication.yml`;
- the page contains no private paths, identifiers or credential-shaped strings.

Negative tests confirm the checker rejects missing paths and unmapped rows. This is documentation only; no product code changes.

Not covered: I did not run the strict MkDocs build locally because `mkdocs` is not installed in the shared environment; it is left to CI.

Validation: `pytest tests/unit/test_openmedkit_threat_model_docs.py tests/unit/test_docs_publication.py -q` (37 passed, 2 skipped), `pytest tests/unit -k "docs or publication or mkdocs or threat or redteam or redactor"` (251 passed, 14 skipped), `ruff check .` and `ruff format --check .` (clean), `scripts/security/check_effect_paths.py --check` (effect_paths_verified), `mypy` (no issues), `pytest tests/ -q -m "not slow and not fuzz" --ignore=tests/unit/training/synthetic/test_dicom_overlays.py` (27000 passed, 224 skipped; the ignored module is a known collection failure on master in the shared environment, which lacks `pydicom`), `scripts/release/check_repo_policy.py --commits origin/master HEAD` (passed).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b7c0322f1b17`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.