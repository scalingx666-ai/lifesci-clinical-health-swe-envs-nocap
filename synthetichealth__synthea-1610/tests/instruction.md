# Issue

**Title:** Upgrade gradle and fix deprecation warnings

## Description

This branch updates gradle to 8.14.3 and addresses all deprecation warnings from the `build.gradle` file.

Support for older java versions is not removed within the gradle 8.x releases. Upgrading to gradle 9.x would remove support for java versions below 17 (https://docs.gradle.org/current/userguide/compatibility.html).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a65f56f13e1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.