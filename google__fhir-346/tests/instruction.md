# Issue

**Title:** Makes protogen.bzl rules include all JSON files in the generated fhir_package, rather than using a hardcoded list.

## Description

Makes protogen.bzl rules include all JSON files in the generated fhir_package, rather than using a hardcoded list.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `91b09ebf0e1d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.