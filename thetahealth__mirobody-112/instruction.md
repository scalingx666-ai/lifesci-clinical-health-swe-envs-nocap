# Issue

**Title:** fix: keep image publish green without page admin scope

## Description

## What changed

The repaired image publish succeeded, but Docker Hub returned 403 while updating repository metadata because the current `DOCKERHUB_TOKEN` can push images without repository-admin page permission.

This keeps normal image releases green after the image is published, emits a clear warning with the required remediation, and keeps `page_only=true` strict so a metadata retry cannot look successful while the page remains unchanged.

## Validation

- `actionlint .github/workflows/docker-hub.yml`
- `ruff check mirobody examples`
- `compileall`
- `lint-imports` — 6 contracts kept, 0 broken
- `pytest -q mirobody/tests/test_skills.py tests/test_doc_paths.py` — 90 passed

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c771647b8d69`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.