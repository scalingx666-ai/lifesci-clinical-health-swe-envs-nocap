# Issue

**Title:** Update sass dev dependencies

## Description

Fixes build errors using latest stable (15), while still staying within our supported Node.js versions (10, 12, 14, 15).

Also replaces `node-sass`, with `dart-sass`, which is recommended by sass-loader and doesn't require a compilation step.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d2e1a96e9726`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.