# Issue

**Title:** Adds primitive handler to base FhirPath validation APIs, and eliminates version-specific APIs.  This will make it easier to expand to future FHIR versions, like R5.

## Description

Adds primitive handler to base FhirPath validation APIs, and eliminates version-specific APIs.  This will make it easier to expand to future FHIR versions, like R5.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d470a22ad14b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.