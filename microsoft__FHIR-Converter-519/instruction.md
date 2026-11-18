# Issue

**Title:** Add ConvertProcessorFactory

## Description

Adds ConvertProcessFactory to return the correct implementation of IFhirConverter depending on the input and output dataTypes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `15a1c7515ed8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.