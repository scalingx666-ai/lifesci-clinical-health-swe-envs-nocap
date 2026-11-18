# Issue

**Title:** Makes FhirPackage.java expose package.json, if one is found.  Use this in ProtoGenerator v2 rather than explicitly passing version metadata.

## Description

Makes FhirPackage.java expose package.json, if one is found.  Use this in ProtoGenerator v2 rather than explicitly passing version metadata.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `84823b2616f4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.