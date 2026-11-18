# Issue

**Title:** Fix an issue in Go FHIR JSON parser where Parameters.parameter.resource fields (or any google.protobuf.Any field with JSON name "resource") could not be parsed or marshaled, failing with "unknown field" errors.

## Description

Fix an issue in Go FHIR JSON parser where Parameters.parameter.resource fields (or any google.protobuf.Any field with JSON name "resource") could not be parsed or marshaled, failing with "unknown field" errors.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a9c25f45d64f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.