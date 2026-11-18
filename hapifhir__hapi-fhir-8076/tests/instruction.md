# Issue

**Title:** Document sendStringParametersAsUnicode=false JDBC requirement for SQL…

## Description

The MS SQL Server JDBC driver sends string parameters as Unicode (NVARCHAR) by default, while the HAPI FHIR schema uses VARCHAR columns. The implicit conversions prevent index usage and can severely degrade query performance. Document the recommended setting in the database support docs and the `HapiFhirSQLServerDialect` javadoc.

Also fix the database support table, which listed the H2 dialect class for MS SQL Server instead of `HapiFhirSQLServerDialect`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9bc6a512d501`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.