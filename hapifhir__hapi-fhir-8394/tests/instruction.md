# Issue

**Title:** Replace http:// test server URLs with https://

## Description

The public HAPI test server has supported HTTPS URLs for a while now. This PR replaces various references in documentation, and points the test overlay at the HTTPS URL.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f9bcab475526`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.