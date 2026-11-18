# Issue

**Title:** Solution 2: Chained search on Citus with uncorrelated branch subqueries (master)

## Description

. This is **solution 2** (#8837), targeting `master` instead of `rel_9_0`. It carries #8824's changes and #8837's on top of them.

### Change
#8824 matches a chained reference's target with an uncorrelated tuple `IN`, but leaves each branch of the chain (contained target, referenced target) as an `EXISTS` correlated to the searched resource `t0`. On Citus, that correlation makes each worker re-scan the shipped target rows for every resource it filters, and unselective chained searches slow down sharply as data grows.

This PR also matches each branch with an uncorrelated tuple `IN` on `t0`'s key:
<pre>
(t0.PARTITION_ID, t0.RES_ID) IN (SELECT s0.PARTITION_ID, s0.RES_ID FROM HFJ_SPIDX_TOKEN s0 WHERE ...)
OR (t0.PARTITION_ID, t0.RES_ID) IN (SELECT s0.PARTITION_ID, s0.SRC_RESOURCE_ID FROM HFJ_RES_LINK s0 WHERE ...)
</pre>
It applies under the same condition as #8824 (PostgreSQL in database partition mode). Other databases keep the correlated `EXISTS`.

This is the "Candidate: uncorrelated branches" SQL from #8824's  section, measured under its  section: 10 to 70 times faster than the other strategies on PostgreSQL and Citus at 20,000 patients.

### Testing
- `DatabasePartitionModeWithPostgresIT` asserts both branches use the uncorrelated `IN` with no `EXISTS` and no correlation to `t0`, and that the search returns the expected resource.
- `TuplePredicateBuilderTest` covers the uncorrelated form on PostgreSQL and the correlated form on SQL Server, Oracle and MariaDB.
- The database partition mode and verification ITs pass on PostgreSQL, SQL Server and Oracle.

Branch: [`ep-2026-11-12-gl9466-uncorrelated-chain-branches-master`](https://github.com/hapifhir/hapi-fhir/tree/ep-2026-11-12-gl9466-uncorrelated-chain-branches-master)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3f77c0353b0b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.