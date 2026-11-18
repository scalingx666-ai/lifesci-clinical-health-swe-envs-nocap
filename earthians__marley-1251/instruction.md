# Issue

**Title:** fix(patient portal): match Vite build output dir to published prebuilt assets path

## Description

Vite was building the patient portal to `healthcare/public/patient_portal/assets`, but the prebuilt-assets CI workflow publishes from `healthcare/public/frontend` (per `pyproject.toml`) — the same directory `index.py` already reads the manifest from at request time. Since Vite never wrote there, the workflow was publishing stale/empty content instead of the real build.

Fix: point Vite's `outDir` at the correct, already-expected directory.

Caught via a Greptile comment on #1245 that was missed before it merged. Verified with a real local build - manifest and bundle now land where they're expected.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5622275d4e59`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.