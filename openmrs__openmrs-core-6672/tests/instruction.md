# Issue

**Title:** Initialize Context's user context holder before its logger

## Description

.

`userContextHolder` is initialized before `log` again, as it was before #6544, and its javadoc now says why the order matters. When creating the logger is what starts log4j, `OpenmrsConfigurationFactory`'s call to `isSessionOpen()` then returns false instead of throwing.

**Tests**
- New: `ContextStaticInitializationTest` loads `Context` in a class loader of its own, where nothing has started log4j, so creating its logger configures logging. On master it fails with the `ExceptionInInitializerError` from #6670. With this change it passes.
- `ContextTest`, `UserContextTest`, `UserContextHasPrivilegeTest` and `DaemonTest` pass, as does the full default api suite: 5605 tests, 0 failures.

**Runtime:** on build 435, Bahmni/openmrs-module-appointments#213's api unit tests get 138 errors and 7 failures on a Mac, once `Context` fails to initialize. Built against this and #6671, they pass there.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a69b14a84bf9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.