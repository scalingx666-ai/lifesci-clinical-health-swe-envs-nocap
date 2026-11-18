# Issue

**Title:** [CI] Use SPM standalone instead of SPM on CI

## Description

Also modified temporarily the cron of the anat pipelines to trigger today.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3fb95738fba1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.