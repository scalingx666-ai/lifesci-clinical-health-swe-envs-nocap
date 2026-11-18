# Issue

**Title:** release: cut 1.5.5

## Description

Cuts 1.5.5. **Stacked on #138: merge #138 first**, then this PR's diff is the one commit.

- `compose.yaml`, the source fallback, `server.json` and the Dockerfile name 1.5.5; `check_versions` passes.
- CHANGELOG's Unreleased becomes 1.5.5.

**e2e before the tag** (`tests/e2e/harness.py`, all five stages, as scope.py asked): passed on an isolated server running this branch, with its own database. 244 readings (1.5.4: 243), no problems; both chat answers cite their rows.

After both merge: tag `1.5.5` → pypi-release.yml publishes PyPI, the GitHub Release and the Docker Hub image; I'll check the PyPI version endpoint and pull the image.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8cd78756f336`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.