# Issue

**Title:** TRUNK-6809: Run the Liquibase status check inside the update scope

## Description

## Description of what I changed

`DatabaseUpdater.executeChangelog` counted the unrun changesets (`StatusCommandStep.listUnrunChangeSets`) *before* entering the Liquibase scope that installs OpenMRS's composite resource accessor (classpath + application data directory, TRUNK-6295). For a changeset that has already run and is `runOnChange="true"`, Liquibase's status check recomputes the checksum (`ShouldRunChangeSetFilter`), and that reads files such as `<sqlFile>` through the current scope's resource accessor (`SQLFileChange.getResource`). Outside the OpenMRS scope that is the thread's root classloader accessor, so a module's sql file isn't found and module startup fails, as Mike saw with Bahmni appointments on 2.8.9.

- `executeChangelog`: count the changesets inside the existing scope (after the lock).
- `getUnrunDatabaseChanges`: run its status check in a `Scope.child` with the same resource accessor.

| Check | Without fix | With fix |
|---|---|---|
| `executeChangelog` second run of a `runOnChange` `<sqlFile>` changeset | fails in `StatusCommandStep.listUnrunChangeSets` ("Resource does not exist") | passes |
| `getUnrunDatabaseChanges` on the same changelog | fails, same cause | passes (nothing left to run) |

The two new tests put the changelog and sql file in the application data directory, which only OpenMRS's composite accessor sees. That reproduces the module case without a real module. Both fail with only the main change reverted.

Note for a 2.8.x backport: the commit doesn't cherry-pick cleanly onto `2.8.x` (conflicts in `DatabaseUpdater` and its test), so it would need a small manual port.

## Issue I worked on

see https://openmrs.atlassian.net/browse/TRUNK-6809

## Checklist: I completed these to help reviewers :)

- [ ] My IDE is configured to follow the code style of this project. (Formatting was applied by Spotless during the build.)
- [x] I have added tests to cover my changes.
- [x] I ran `mvn clean package` right before creating this pull request (BUILD SUCCESS).
- [x] All new and existing tests passed (api: 5,606, web: 309, 0 failures).
- [x] My pull request is based on the latest changes of the master branch.

---
🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5eb8cba2e30b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.