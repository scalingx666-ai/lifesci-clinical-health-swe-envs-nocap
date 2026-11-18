# Issue

**Title:** Add multimodal privacy and device release gates

## Description

## Description

.

Execute public synthetic OpenPHI-Vision controls and measure local EdgeHealthBench workloads instead of inferring multimodal readiness from unit tests or a demonstration. Critical burned-in or document-any-PHI leakage always fails independently of quality, utility, abstention and device performance.

## Changes

- Generate and execute seven bounded tracks: rendered documents, images, native RGB DICOM previews, WSI labels/overviews, OCR conflicts, mixed languages and cross-document identity. Inspect actual whole PNG exports and metadata, retaining only hashes and aggregate evidence.
- Keep quality (structural routing), utility (public control pixels) and abstention separate, with per-track/language counts and descriptive Wilson intervals. Invalid outputs, missing tracks and entirely unassessed candidates cannot pass.
- Execute bounded device callbacks with independent latency, throughput, RSS, allocator-memory, thermal, CPU-time proxy, reference/repeat parity and privacy gates. Warmup leakage fails; unavailable tiers remain `not_run`; accelerator profiles require separate allocator evidence.
- Bind model, preprocessing, dataset, harness, hardware/runtime declarations, policy and license snapshots. License metadata records provenance without an allowlist or runtime terms acceptance.
- Add executable guides, navigation and changelog entries. No new package dependency is introduced beyond the existing prerequisite PRs.

The included known-layout control proves redaction/routing wiring, not model recognition or clinical recall. The CPU example is a development smoke profile. Public fixtures are not independently validated or contamination-resistant; thermal/GPU/energy evidence is never invented, and no report grants clinical readiness. Trusted provider callbacks are not an OS sandbox.

## Dependencies

Built from current `master` (`29ffa7005`) and preserves the existing histories of #4416 (including #4408), #4417, #4390, #4411, #4406 and #4398. Their prerequisite changes remain visible until those PRs land. The feature itself changes eight files. Original PR branches are unchanged.

## Validation

- 32 focused controls passed on Python 3.12 and frozen Python 3.11, covering moved/metadata leakage, blackout utility loss, abstention, cancellation, changed provenance, warmup leakage, missing/stale resources, allocator budgets and exact parity.
- Full Python suite: 26,710 passed, 157 skipped and 11,380 subtests passed. The only two failures were new-guide publication ordering; corrected the manifest and reran both complete test files: 52 passed and 25 subtests passed.
- Both guide examples executed successfully under OS-level network denial, including 21 actual synthetic cases and one warmup plus three measured CPU trials. Performance numbers are smoke evidence under concurrent validation load, not a qualified device benchmark.
- `make format`, `make lint`, `make format-check`, `make type-check`, explicit mypy on both modules, public API compatibility and all scoped pre-commit hooks passed.
- Strict `make docs-build` passed, including final Pages route, asset, metadata and feed validation.
- Wheel/sdist build and Twine checks passed; both artifacts contain byte-exact final suite source.
- Prerequisite dependency lock is unchanged from the already validated combined native environment; no new dependencies. Complete incoming commit attribution is checked before push. Hosted checks will run on this PR head.

Type: feature, evaluation controls and documentation. Python evaluation harness only; existing backend and Swift contracts are unchanged. No restricted weights or datasets are bundled.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8bb6f88f7509`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.