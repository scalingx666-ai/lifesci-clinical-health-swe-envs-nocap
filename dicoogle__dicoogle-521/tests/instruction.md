# Issue

**Title:** Replace service status signal implementation

## Description

Instead of a canvas, use a CSS decorative circle to indicate whether a service is online.

This implementation is simpler and has better rendering quality.
![Capture-dicoogle-service-status-css](https://user-images.githubusercontent.com/4738426/136394021-b27bf10d-4acd-4c91-acbc-0dbdce62c49f.PNG)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5507ee7d8b8b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.