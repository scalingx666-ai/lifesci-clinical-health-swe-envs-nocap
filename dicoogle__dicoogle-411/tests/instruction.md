# Issue

**Title:** Add Java EE modules for Java 11 support

## Description

Fix #410

- explicitly add `jaxb-api` module to pom.xml
- [Travis CI] disable allow_failures on openjdk11

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b01d62dee188`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.