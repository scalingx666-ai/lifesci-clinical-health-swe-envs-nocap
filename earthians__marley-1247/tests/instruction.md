# Issue

**Title:** ci: Publish prebuilt assets for Pilot (version-15-hotfix)

## Description

Same change as  for `version-15-hotfix`.

See [Prebuilt Assets](https://github.com/frappe/pilot/blob/develop/docs/prebuilt-assets.md).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `41f05060a69f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.