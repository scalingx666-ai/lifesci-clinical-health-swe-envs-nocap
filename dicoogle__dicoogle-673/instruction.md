# Issue

**Title:** Include submitted query and provider in “result-selection-ready” event

## Description

This PR adds the submitted query and provider to the `result-selection-ready` event as a new `request` field.

This further enriched the data that `result-batch` web plugins have access to.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0a514aac7115`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.