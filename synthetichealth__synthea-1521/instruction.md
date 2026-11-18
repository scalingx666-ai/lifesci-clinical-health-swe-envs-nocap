# Issue

**Title:** ICD-10-CM Code Mapping

## Description

1. Add support for mapping condition codes to ICD-10-CM in the FHIR R4 exporter.
2. Fix some checkstyle warnings.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `76f2925bbcb0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.