# Issue

**Title:** Automated Migration Testing (HAPI-FHIR) V8_12_0

## Description

Migration test scripts added/changed in scope of this PR:

V8_12_0
- [x] New table: `BT2_JOB_ATTACHMENT`.
- [x] New table: `BT2_JOB_ATTACHMENT_CHUNK`.
- [x] Updated: `TRM_CODESYSTEM_VER` table. Added `CS_INTENDED_VERSION_ID` column.
- [x] Updated: `TRM_VALUESET` table. Added `VS_INTENDED_VERSION_ID`, `EXPANSION_ERROR` columns.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2e914832f45e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.