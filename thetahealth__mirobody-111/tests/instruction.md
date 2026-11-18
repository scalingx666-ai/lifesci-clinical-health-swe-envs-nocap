# Issue

**Title:** fix: validate images and sync Docker Hub metadata

## Description

## What changed

- Add an installed-package smoke test to the Docker builder. It runs outside `/src`, checks `BUNDLE_VERSION`, and resolves hemoglobin before either platform is published.
- Fix Docker Hub page synchronization to use the current `/v2/auth/token` and `/v2/repositories/:namespace/:repository` endpoints.
- Split page sync into its own job and add `page_only=true` for metadata-only retries.
- Keep the reviewed `source_ref` repair rebuild path for the existing `1.5.3` tag.

The first repair rebuild already proved the image path: both platforms published and inspect successfully, and the public `1.5.3` image imports the real package. Only the page PATCH returned 403; this PR fixes that exact failure.

## Validation

- `actionlint .github/workflows/docker-hub.yml`
- synthetic authenticated page-sync request test
- `docker run --rm --platform linux/amd64 thetahealth4mirobody/mirobody:1.5.3 ...` — installed wheel import and resolve pass
- `pytest -q mirobody tests/test_doc_paths.py` — 224 passed, 13 xfailed
- `ruff`, `compileall`, `lint-imports` — 6 contracts kept, 0 broken

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `121d784524e5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.