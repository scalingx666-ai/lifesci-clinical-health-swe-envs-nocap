# Issue

**Title:** #6189 Add configurable transaction isolation level to DataService

## Description

Refactors DataService.executeStatement()/executeStatements() to run under an optional isolation level (READ COMMITTED) instead of always using the connection's default (REPEATABLE READ). Applied to buildTransactionFact()/buildConsumptionFact() in ReportService, since MariaDB/MySQL take shared next-key locks on every row read during an INSERT...SELECT under REPEATABLE READ (which was the root cause of recurring Lock wait timeout exceeded errors on transaction/transaction_entry during the nightly RefreshTransactionFactJob run).

Also fixes the underlying atomicity bug: executeStatements() now runs its statement list as a single transaction and rethrows on failure, instead of running each statement independently and silently swallowing exceptions (partial fix for OBS-1987; full fix for DDL-containing sequences tracked separately in #6190).

 (ETL refresh causes lock wait timeout) 
References: 
- OBS-1988 Lock wait timeout exceeded / for all transactions
- OBPIH-3641 Discovery: General improvements related to analytics ETL process

Targets `release/0.9.9-hotfix1`. This was originally stacked on #6188 (#6186 support multiple development environments) because I tested it from a git worktree, which needs that fix to run locally. #6188 is a development-only change, so it has been left out of this PR: the branch was rebased onto `release/0.9.9-hotfix1` with only the two #6189 commits, and #6188 stays a separate PR against `develop`.

~Depends on PR #6188 (#6186 support multiple development environments) - need to stack it because i was using a worktree for the current PR and I was unable to test locally without the changes from #6188.~
~Note: Because it's a stacked PR, that means it would be best to have #6188 merged (not squash-merged), I think. However, if it does get squash-merged, apparently you can you use `git rebase --onto` to merge just the commits that are unique to #6189 onto the develop branch. Apparently, a normal rebase would match commit SHAs. So the process should look something like this. The `--force-with-lease` is apparently safer than `--force` (in case others have~
~`git rebase --onto origin/develop origin/chore/6186-support-multiple-development-environments 6189-lock-wait-timeout`~
~`git push --force-with-lease origin 6189-lock-wait-timeout`~

Note: By the way, I accidentally used the same commit message in both commits and had already pushed the changes to remote so decided not to amend. The second commit was just a fix for the `sql.connection` dereference causing a NPE. I forgot to change the commit message, but it probably should have said something like `Fixed NPE with sql.connection - connection is null until first use`. The use of `cacheConnection` will obtain an actual live database connection, so we can set the isolation level properly.

Follow-ups:
- [ ] Create an issue to build staging tables and swap using `RENAME TABLE` (If the nightly fact table refresh (RefreshTransactionFactJob) fails partway through, reports show no data until the next successful run. `truncate` commits immediately, so a failure can't be rolled back).
- [ ] Update issue #6190 to correct what it says re: the fact table rebuilds are fixed by #6189 (We switched from `delete` to `truncate`, so they still have the same problem as the other refreshes).
- [ ] Detect when the analytics tables are in a bad shape and emit an event (Current code already alerts via Sentry but if want resilience we can add a retry mechanism when it fails.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a19378538056`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.