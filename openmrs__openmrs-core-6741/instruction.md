# Issue

**Title:** TRUNK-6842: Void encounter providers after the encounter void details are set

## Description

.

## Description of what I changed
In `EncounterServiceImpl.voidEncounter`, the encounter providers are now voided after the encounter's `voidedBy`, `dateVoided` and `voidReason` are set, instead of before.

When `voidEncounter` is called from within the API, for example by `transferEncounter`, AOP is bypassed and the encounter's `voidedBy`/`dateVoided` are still null when the old loop ran. The encounter providers were then voided with null void details. `VoidSaveHandler` later filled these in on save with a new timestamp, which can differ from the encounter's `dateVoided`. When they differ, the unvoid handler won't restore those encounter providers.

#6739 (2.9.x) and #6740 (master) already include this change.

## Issue I worked on
https://openmrs.atlassian.net/browse/TRUNK-6842

## Checklist: I completed these to help reviewers :)
- [ X ] My IDE is configured to follow the [**code style**](https://wiki.openmrs.org/display/docs/Java+Conventions) of this project.
- [ X ] I have **added tests** to cover my changes. (Covered by the existing `transferEncounter_shouldVoidEncounterProvidersOfGivenEncounterButNotTheirProviders` assertion that the dateVoided values match.)
- [ ] I ran `./mvnw clean package` right before creating this pull request. (Ran `mvn test -pl api -am -Dtest='Encounter*Test'` instead: 276 run, 0 failures; the formatter made no changes.)
- [ X ] All new and existing **tests passed** (Encounter*Test locally; full suite left to CI).
- [ X ] My pull request is **based on the latest changes** of the 2.8.x branch.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a48b9df9f870`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.