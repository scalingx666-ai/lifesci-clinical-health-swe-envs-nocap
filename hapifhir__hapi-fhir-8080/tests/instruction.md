# Issue

**Title:** Fix delete-expunge SQLGrammarException on SQL Server in database part…

## Description

When Database Partition Mode is enabled, DeleteExpungeSqlBuilder emits DELETE statements using row-value constructors — WHERE (PARTITION_ID,RES_ID) IN ((1,2353),...) — which SQL Server does not support in IN predicates, so every $delete-expunge batch job failed with a SQLGrammarException.

On MSSQL (detected via DialectSvc, now injected into the builder), the PIDs are grouped by partition and emitted as WHERE (PARTITION_ID = 1 AND RES_ID IN (2353,2354)) OR (PARTITION_ID = 2 AND RES_ID IN (99)), following the precedent of SearchBuilder#loadCurrentResourceVersionsForMsSqlDbpm. SQL generated for all other databases, and for non-partitioned mode, is unchanged.
  
  Testing

- Unit tests in DeleteExpungeSqlBuilderTest assert the generated SQL for MSSQL+DBPM, non-MSSQL DBPM, and non-DBPM (test class relocated to match the
  builder's package for access to the package-private method)
- End-to-end test in DbpmEnabledTest runs the delete-expunge batch2 job in forced-MSSQL mode across two partitions and verifies the emitted DELETE
  statements and that resources are expunged

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fa2a5762cd68`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.