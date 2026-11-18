# Issue

**Title:** ci: Publish prebuilt assets for Pilot

## Description

## Summary
Build the Health assets in CI and publish them on the release `assets-<branch>`. Pilot benches download them and skip the asset build, the slowest and most memory-hungry step of an install or update.

## What changed
- Add the `Pre-build assets` workflow for pushes to `develop`, `version-15` and `version-16`.
- Declare the SPA build output in `[tool.bench.assets]`: `patient_portal` builds `healthcare/public/frontend`.

Backport: separate PRs #1246 (`version-16-hotfix`) and #1247 (`version-15-hotfix`).

See [Prebuilt Assets](https://github.com/frappe/pilot/blob/develop/docs/prebuilt-assets.md).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8e7978037b81`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.