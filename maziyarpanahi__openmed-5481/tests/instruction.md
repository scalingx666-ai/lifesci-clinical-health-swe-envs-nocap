# Issue

**Title:** Build a real-device qualification harness for portable kit runtimes

## Description

. Depends on #4452.

This adds `openmed.eval.kit_qualification`, a collector that produces the `device-run` evidence kind for the frozen kit support matrix. A versioned qualification plan pins bundle, fixture and policy digests plus explicit gates for chosen matrix cells. It expands into bundle × runtime/provider × platform version × precision × fixture × policy targets. Closed, value-free evidence records from device, simulator, emulator or fake-runtime runs are matched to those targets. The report flags unplanned cells, missing targets, stale bundle/fixture/policy/harness digests, runtime-version and cell-definition drift, and each failed gate on its own: recall, leakage, cold, warm and sustained latency, cancel latency, memory against the tier RAM ceiling, allocator memory, thermal, energy and provider fallback. Only physical-device evidence can qualify a target; simulator, emulator and fake-runtime records are counted and labelled separately. The gates reuse the EdgeHealthBench rules (`not_run` never passes, zero-leak, `missing_resource_evidence`, energy proxies labelled). `edge_health` gains Android ORT CPU/NNAPI/QNN and iOS-family device tiers, a shared allocator-tier set and its failure-code vocabulary. `scripts/release/kit_qualification_report.py` writes the report and, when asked, a digest-bound proposal and a proposed matrix copy. It never writes the committed matrix; supported cells that fail are listed for review, not demoted. `openmed.eval.kit_support_matrix` exposes `identifier_shaped`, and its Samsung model-code pattern now also catches suffixed codes such as `SM-G991B`. New page: `docs/openmedkit-device-qualification.md`.

Not covered: actual qualification runs on physical iOS and Android devices (maintainer-run). No device-run evidence is committed and no matrix cell changes status in this PR. The harness cannot attest that a record came from the hardware it names; execution type and device class are runner declarations.

Validation: `pytest tests/unit/eval/test_kit_qualification.py tests/unit/eval/test_kit_support_matrix.py tests/unit/eval/test_multimodal_release_gates.py tests/unit/test_docs_publication.py tests/unit/release/test_public_api_compat.py -q` (all passed), `pytest tests/ -q -m "not slow and not fuzz" --ignore=tests/unit/training/synthetic/test_dicom_overlays.py` (27161 passed, 224 skipped, 298 deselected; `test_dicom_overlays.py` cannot be collected without `pydicom`), `ruff check .` and `ruff format --check .` (clean), `python scripts/security/check_effect_paths.py --check` (verified), `mypy` (no issues), `python scripts/release/check_kit_support_matrix.py` (ok). The strict MkDocs build is left to CI.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `174fd485c153`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.