# Issue

**Title:** Rebuild IDX_RES_TYPE_FHIR_ID with PARTITION_ID in database partition mode (MSSQL)

## Description

.

On Microsoft SQL Server in database partition mode, the `FHIR_ID` collation-fix migration recreated the unique index `IDX_RES_TYPE_FHIR_ID` as `(RES_TYPE, FHIR_ID)`, dropping `PARTITION_ID` and thereby enforcing global instead of per-partition uniqueness of resource type/id.

This adds a corrective migration (`20260724`, V8_12_0) that, in database partition mode on SQL Server, rebuilds `IDX_RES_TYPE_FHIR_ID` as `(PARTITION_ID, RES_TYPE, FHIR_ID)`. The drop is guarded to run only when `PARTITION_ID` is not already a key column, so already-correct databases are not rebuilt.

### Tests
`HapiSchemaMigrationTest`:
- **Fresh install** (partition and non-partition modes): the index columns match the mode.
- **Upgrade of an existing 8.8.0+ database** (case-sensitive collation + 2-column index): the index is rebuilt to include `PARTITION_ID`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fd2a1696c613`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.