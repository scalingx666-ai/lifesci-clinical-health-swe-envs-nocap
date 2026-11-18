# Issue

**Title:** feat(core): add createStaticClient for rendering from in-memory resources

## Description

`createStaticClient` returns a `MedplumClient` that serves reads by type and id from a list of resources, with no network access. Other requests fail with "Not supported by static client". This lets apps render Medplum components such as `DiagnosticReportDisplay` from resources gathered up front.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `67418132c867`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.