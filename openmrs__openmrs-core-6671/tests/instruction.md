# Issue

**Title:** Read the name layout global properties with a proxy privilege

## Description

.

`NameSupport` now reads `layout.name.template` and `layout.name.format` with "Get Global Properties" added as a proxy privilege, the way `OpenmrsConfigurationFactory`, `OpenmrsLoggingUtil` and `OpenmrsPropertyLookup` read theirs. Formatting a name no longer depends on whether the viewer may read global properties, so `PersonName.getFullName()` and `Provider.getName()` work for every user again, and they use the configured layout.

I didn't catch `AccessDeniedException` in `getFullName()` instead, next to `APIException`. That would restore 2.x's behaviour, where a user without the privilege gets the built-in format rather than the configured one. Until a privileged user initializes `NameSupport`, each of that user's calls would also retry `init()`, which registers the global property listener again.

**Tests**
- New: `NameTemplateTest.shouldUseNameTemplateConfiguredViaGlobalPropertiesForAUserWithoutGetGlobalProperties`. It configures a template through the global properties, resets `NameSupport` so that it initializes as a user with no roles, and calls `getFullName()` as that user.
  - On master it fails with the `AuthorizationDeniedException` from #6669, in `NameSupport.init`.
  - Reverting either read to a plain `getGlobalProperty` call fails it again, at `init` or at `getDefaultLayoutFormat`.
- The full default api suite passes: 5605 tests, 0 failures.

**Runtime:** Bahmni/openmrs-module-appointments#213's `AppointmentsServiceTest.shouldFetchAppointments` fails on build 435 at `provider.getName()`. Built against this and #6672, the module's api tests pass, in a Linux container and on a Mac.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a69b14a84bf9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.