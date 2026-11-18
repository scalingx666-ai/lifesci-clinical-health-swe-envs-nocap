# Issue

**Title:** server: /mirobody.json carries capability_version

## Description

## Capability document for headless clients

`/mirobody.json` now serves `capability_version` and `server_version` whether or not a web client is mounted. An existing `MIROBODY_WEB_CONFIG` overlay keeps precedence. The static frontend mount stays in `start()`.

Updated against the 1.5.2 main branch. Verified a headless `Server` responds to GET and HEAD with the expected keys; 19 frontend serving tests pass; Ruff, compileall and six import contracts pass. Current GitHub checks are shown in the PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `34734afa16db`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.