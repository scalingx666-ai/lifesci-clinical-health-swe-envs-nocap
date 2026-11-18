# Issue

**Title:** [8750] delete stale HFJ_RES_SEARCH_URL entries with one bounded DELETE per page

## Description

**Background**

 (fixing  released in 8.12.0) replaced the cleanup's single unbounded DELETE on HFJ_RES_SEARCH_URL with small pages, each in its own transaction, so a large table no longer causes a statement timeout. Each page still took two statements: a select of the stale IDs, then a delete of those IDs.

**Changes**
- Each page is now one bounded `DELETE` (HQL `DELETE … WHERE RES_ID IN (SELECT … WHERE CREATED_TIME < :cutoff ORDER BY CREATED_TIME LIMIT :limit)`). Hibernate renders the limit per database: `TOP (?)` on MSSQL, `FETCH FIRST ? ROWS ONLY` on H2, Postgres and Oracle. No rows are read or locked ahead of the delete, and a page never takes a table lock.
- A sweep stops at the first page that deletes fewer rows than the batch size.
- New `JpaStorageSettings#setSearchUrlCleanupBatchSize(int)`: rows deleted per transaction, default 1,000, between 500 and 2,000 (replaces the hard-coded 1,800).
- `IResourceSearchUrlDao.findStaleIds(Date, Pageable)` is replaced by `deleteStaleEntries(Date, int)`.

**Tests**
- `SearchUrlMaintenanceSlowDeleteMsSqlIT`: new test that runs the cleanup at the maximum batch size and checks SQL Server recorded no lock escalation on the table (`sys.dm_db_index_operational_stats`). The existing 100K-row drain test still passes under the 1 s statement timeout.
- Unit tests for the paging loop and the new setting.
- Checked by hand, not added as a test: on H2, Postgres, MSSQL and Oracle 23ai, each page runs as a single `DELETE` with no separate select, and only stale rows are removed.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0a22bf8bebb1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.