# Issue

**Title:** release: 1.4.3

## Description

Cuts 1.4.3: the version literal in `mirobody/__init__.py` and the CHANGELOG's
top entry, which the suite pins to each other and the release workflow checks
against the tag. No code changes — the twenty-two commits are already on `main`
via #76.

## What the release contains

A reading extracted from an uploaded report now carries a LOINC code, which is
the headline promise and did not hold for the main way readings arrive.
`mirobody.pulse` becomes `mirobody.collect` and `kernel.vendors` becomes
`kernel.decoders`, so every package is named after the stage it implements. An
Apple Health export imports without the mobile app.

## Verified

- Full local suite: 1,700 passed, 4 skipped. Clone suite: 33, exit 0.
- ruff, comment style, 4 import-linter contracts, bundle-version and
  runtime-index `--check`: all clean.
- `python -m build` + `check_wheel_data.py`: 8 data bundles present, no
  build-only artifact or test module in either artifact. Wheel ships 107 files
  under `mirobody/collect/` and none under the old name.
- The three wheel gates, run verbatim from `pypi-release.yml` against the built
  wheel: ① library install reaches numpy only (`deps []`), ② `[parse]` imports
  clean with no FastAPI, ③ the engine/agent boundary holds on a langchain-free
  server install.
- On the bare library install, from outside the repository: version 1.4.3,
  bundle `loinc-2.82+2026.08.28-af2524b7a285`, offline resolve in four
  languages, and `mirobody import apple` on all three documented input shapes
  (zip, export.xml, unpacked directory) plus `--out`.
- `benchmarks/run_eval.py --no-embed`: 7,354 cases, coverage 0.963, wrong-rate
  0.032 — unmoved.

## Not verified

No local Postgres in this session, so `scripts/e2e_health_data.py` and the
five-stage end-to-end walk did not run. The identity funnel is pinned by unit
tests only; the `0 of 130 → 130 of 130` figure comes from the external report,
not from a run here.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f7f11b9a7f74`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.