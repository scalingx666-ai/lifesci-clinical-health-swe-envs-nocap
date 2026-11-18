# Issue

**Title:** fix(frontend): stop 500 after deploys and 404 on logout

## Description

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Bug Fixes**
  * The version displayed in the app now matches the packaged application version, rather than the framework’s build identifier. Framework build metadata continues to use its own build version, keeping the displayed product version distinct from the version used to identify a particular build. This makes the version shown in the app consistent with the application release.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ba666219ba41`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.