# Issue

**Title:** Makes C++ FhirPackage fail only on fatal parse errors.  This makes Package loading lenient towards regex failures like overly long ids, which many external validators do not enforce.

## Description

Makes C++ FhirPackage fail only on fatal parse errors.  This makes Package loading lenient towards regex failures like overly long ids, which many external validators do not enforce.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0d7bca220e83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.