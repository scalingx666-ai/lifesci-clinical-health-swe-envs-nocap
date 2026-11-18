# Issue

**Title:** TRUNK-6765: Replace Joda-Time with java.time and drop the dependency

## Description

# Description of what I changed

This PR replaces Joda-Time with `java.time` in `ConceptReferenceRangeUtility` and its test.

Changes:
- Replaced `org.joda.time.LocalTime` with `java.time.LocalTime`
- Added `Clock` injection for testability
- Added boundary tests (midnight, 23:59,)
- Removed `joda-time` dependency from POMs and BOM
- Wired the injected clock through all date/time-producing paths in `ConceptReferenceRangeUtility` (`getDays`, `getWeeks`, `getMonths`, `getYears`, `getPatientPrograms`, `isInProgramState`, `toLocalDate`) so a fixed test clock is honored consistently rather than falling back to the real system clock in some spots
- Removed the stale `joda-time` entry from `NOTICE.md`

# Issue

https://openmrs.atlassian.net/browse/TRUNK-6765

# Testing

- Ran `mvn test -Dtest=ConceptReferenceRangeUtilityTest -pl api -am`
- All 74 tests pass ✅
- Verified no `org.joda` imports remain
- Verified Joda-Time removed from all POMs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f2991bda233f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.