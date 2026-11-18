# Issue

**Title:** Move Container Build Process to generic

## Description

The current container build process depends upon `ENCRYPTION_KEY` which needs to exist at build time, this process modification generates ENCRYPTION_KEY unique to each build. The user is still responsible for generating their own encryption key and inputting it via environment vars.

The `ARG DATABASE_URL` is not required for build and works via environment variables, this has been removed. The ARG is fully tested in my environment minus my  issue. I need this resolved to fully test the `ENCRYPTION_KEY` changing upon builds though I do not see an issue with it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6d9169239c5d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.