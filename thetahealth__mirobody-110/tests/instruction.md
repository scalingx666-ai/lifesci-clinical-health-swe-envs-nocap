# Issue

**Title:** fix: publish skill evidence and refuse category terms

## Description

## What changed

The merged 1.5.3 tree had two public correctness gaps:

- `mirobody/tests/test_skills.py` was described as release evidence but the build backend removed it from every wheel.
- Six generic category/specimen terms still selected specific LOINC assays: `免疫`, `stool`, `重金属`, `heavy metals`, `激素`, and `enzymes`.

This change keeps only `test_skills.py` in wheels, preserves the full test directory in sdists, and makes the six terms explicit resolver refusals through the existing override mechanism. It updates the skill reference, testing docs, and changelog together.

The Docker workflow now also syncs the checked-in Docker Hub description and supports a manual repair rebuild from `source_ref=main` while retaining the requested version tag.

## Validation

- `ruff check mirobody examples`
- `python -m compileall -q mirobody`
- `pytest -q` — 3177 passed, 59 skipped, 13 xfailed
- `lint-imports` — 6 contracts kept, 0 broken
- `python -c "import mirobody.kernel.meds, mirobody.kernel.query"`
- `uv build --wheel --sdist` + `scripts/check_wheel_data.py`
- wheel contains only `mirobody/tests/test_skills.py` under the test path

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7c5360a0759a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.