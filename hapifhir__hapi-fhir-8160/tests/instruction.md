# Issue

**Title:** 8159 failed to get sql log file

## Description

.

## Summary

Fixes a `FileNotFoundException` that occurred when enabling Hibernate SQL logging while running from a packaged JAR. `SqlLoggerFilteringUtil` loaded the SQL log filter file via `ClassPathResource.getFile()`, which fails for resources inside a JAR since they have no filesystem `File`.

## Changes

- Read the filter file as a classpath stream (`getInputStream()`) instead of resolving it to a `File`, so it works both on the filesystem and when packaged in a JAR.
- Added a regression test that packages the filter file inside a JAR and verifies the lines are read correctly.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3fe390036239`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.