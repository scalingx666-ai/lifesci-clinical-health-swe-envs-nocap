# Issue

**Title:** Refactor ConvertProcessorFactory and add UnitTests

## Description

Remove ConvertTelemetryConfiguration class and allow code user to pass in ProcessorSettings, so they can configure the EnableTelemetryLogging field.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fa11e12b7ab5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.