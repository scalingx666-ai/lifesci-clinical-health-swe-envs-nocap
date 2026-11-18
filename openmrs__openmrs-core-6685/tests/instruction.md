# Issue

**Title:** TRUNK-6809: Run the Liquibase status check inside the update scope (2.8.x)

## Description

## Description of what I changed

Backport of #6679 to `2.8.x`. The commit doesn't cherry-pick cleanly (formatting conflicts in `DatabaseUpdater` and its test), so it was ported by hand; the behavior and tests are the same as on master. Authorship is kept with the original author.

`DatabaseUpdater.executeChangelog` counted the unrun changesets before entering the Liquibase scope that installs OpenMRS's composite resource accessor. For an already-run `runOnChange` changeset, Liquibase's status check recomputes the checksum and reads files such as `<sqlFile>` through the current scope's accessor. Outside the OpenMRS scope, module files aren't found and module startup fails.

- `executeChangelog`: count the changesets inside the existing scope (after the lock).
- `getUnrunDatabaseChanges`: run its status check in a `Scope.child` with the same resource accessor.

## Verification on 2.8.x

- `DatabaseUpdaterTest`: 8/8 pass with the change. On unpatched `2.8.x` the two new tests fail with `UnexpectedLiquibaseException: Resource does not exist` from `StatusCommandStep.listUnrunChangeSets`.
- Restored a backup of a long-running PIH test server (most `liquibasechangelog` rows have `8:` checksums) into the PIH Sierra Leone distro image, which includes Bahmni Appointments 2.2.0:
  - **2.8.10:** Bahmni Appointments fails to start: `FileNotFoundException: The file patientPastAppointments.sql was not found in the configured search path` from `SQLFileChange.generateCheckSum` / `ShouldRunChangeSetFilter.checksumChanged`.
  - **2.8.11-SNAPSHOT + this change, first start:** starts cleanly. The appointments changesets match their stored checksums and aren't re-run. The only new changeset is the core `TRUNK-6549-2026-06-07`, already on `2.8.x`.
  - **Second start:** starts cleanly. Only `runAlways` changesets re-run. The changelog row count and checksum mix are unchanged, and the lock is released.

## Issue I worked on

see https://openmrs.atlassian.net/browse/TRUNK-6809

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4d6340a8d87b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.