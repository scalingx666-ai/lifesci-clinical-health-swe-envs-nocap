# Issue

**Title:** Fail the SNAPSHOT deploy job if the version is not a SNAPSHOT

## Description

SNAPSHOT pipelines never verified whether the artifact it was about to publish was a SNAPSHOT or not. This means if the version was, for example `8.12.0`, the pipeline would publish this full release.

This PR fixes this by adding a check for the `-SNAPSHOT` suffix before proceeding with the pipeline. If it is absent the pipeline now exits and logs an error message.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0d098b2e9a58`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.