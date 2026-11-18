# Issue

**Title:** Improve Travis CI configurations

## Description

- add `openjdk10` and `openjdk11` target
- remove `jdk9`, since it's no longer maintained (users are advised to move to jdk10 ASAP)
- configure Node.js variants 6 and Stable to only build the webapp (slightly faster builds)
- fix Travis CI builds on jdk 10 and 11 (only install extra cacerts on jdk 8)
- only allow build failures on JDK 11

All builds on Travis CI now pass except for JDK 11 due to the decoupling of certain `javax` modules from the standard library. Fixing the issues in this version is currently in low priority.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8748eac7e071`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.