# Issue

**Title:** Enmasse server url

## Description

Allow enmasse to be passed a server url.

In my case, gunicorn_bind contained 0.0.0.0, which broke enmasse.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3315fc6e624a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.