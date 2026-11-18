# Issue

**Title:** TRUNK-6809: Run the Liquibase status check inside the update scope (2.9.x)

## Description

## Description of what I changed

Backport of #6679 to `2.9.x`. The master commit doesn't apply cleanly, so this cherry-picks the `2.8.x` backport (#6685), which applies without conflicts. Authorship is kept with the original author.

`DatabaseUpdater.executeChangelog` counted the unrun changesets before entering the Liquibase scope that installs OpenMRS's composite resource accessor. For an already-run `runOnChange` changeset, Liquibase's status check recomputes the checksum and reads files such as `<sqlFile>` through the current scope's accessor. Outside the OpenMRS scope, module files aren't found and module startup fails.

- `executeChangelog`: count the changesets inside the existing scope (after the lock).
- `getUnrunDatabaseChanges`: run its status check in a `Scope.child` with the same resource accessor.

## Verification on 2.9.x

- `DatabaseUpdaterTest`: 8/8 pass with the change. On unpatched `2.9.x` the two new tests fail with `UnexpectedLiquibaseException: Resource does not exist`.
- The end-to-end before/after (Bahmni Appointments failing to start on a restored long-running server's database, then starting cleanly with the fix on a first and a second run) was done on `2.8.x`; .

## Issue I worked on

see https://openmrs.atlassian.net/browse/TRUNK-6809

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4cc6f8e43ce5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.