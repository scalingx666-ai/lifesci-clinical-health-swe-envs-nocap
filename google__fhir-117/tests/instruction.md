# Issue

**Title:** Clean Up Includes For fhir_package

## Description

Clean Up Includes For fhir_package

- Update stale includes for fhir_package .h and .cc
- Use correct types la_int64_t and la_ssize_t when interacting with libarchive
  rather than int64.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a7c494ee0524`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.