# Issue

**Title:** release: cut 1.5.4

## Description

Cuts 1.5.4. After merge: tag `1.5.4` on the merge commit, which runs `pypi-release.yml` (PyPI, GitHub Release) and calls `docker-hub.yml` (multi-arch image `thetahealth4mirobody/mirobody:1.5.4` + Docker Hub page from `docs/docker-hub-description.md`).

## What changes

- **release: cut 1.5.4**: `compose.yaml` (both app services), the source `__version__` fallback, `server.json` and the Dockerfile default name 1.5.4; CHANGELOG's Unreleased becomes 1.5.4. `scripts/check_versions.py` passes.
- **docs**: #123 measured the large size on the 24 questions, but `local-models.md` and its zh edition still said it had not run. They now carry 20.8 GB, 138 s, 22 of 24 (240/248) and the same-machine comparison with the small size (229).
- **Social card**: the old card said 296/296 and used the pre-1.5.4 pitch. It now shows the README's headline, the two ways to run it, and a frame of the product (`social-preview.png`, 2560×1280, 527 KB). It still has to be uploaded in Settings.

## Verified

- README/doc gates, engine coverage and skills: 249 passed.
- A clean `uv` venv installs `-e '.[app]'` with deepagents 0.7.23 and imports the agent.
- The five-stage e2e runs on an isolated 1.5.4 server and worker (own database, port 18190); result posted below before tagging.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `053187471122`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.