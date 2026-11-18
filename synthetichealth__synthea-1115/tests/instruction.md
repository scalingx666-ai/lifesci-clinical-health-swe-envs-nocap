# Issue

**Title:** Add new attribute to RIF manifest.

## Description

This tiny PR adds a new `syntheticData` attribute to the RIF manifest as requested by the BFD team.

See https://github.com/CMSgov/beneficiary-fhir-data/blob/master/apps/bfd-pipeline/bfd-pipeline-ccw-rif/src/main/resources/bfd-manifest.xsd

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d4af94570aba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.