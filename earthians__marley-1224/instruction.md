# Issue

**Title:** fix: restrict fee validity lookup to authorized roles

## Description

This fix already shipped in a release via the hotfix backport PR #1220 , but was never cherry-picked into `develop`, so `develop` has been missing it since. This PR carries the same fix over so `develop` doesn't regress it on the next release cut.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e0fed51fed95`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.