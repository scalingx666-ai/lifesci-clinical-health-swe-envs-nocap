# Issue

**Title:** TRUNK-6848: Reject invalid dates and times in Obs.setValueAsString for DT and TM datatypes

## Description

## Description of what I changed

Ticket: https://issues.openmrs.org/browse/TRUNK-6848

The DT and TM branches of Obs.setValueAsString parsed with a SimpleDateFormat in its default lenient mode, and DateFormat.parse does not require the whole string to be consumed. Invalid values were silently converted and stored as the obs value_datetime: "2023-02-30" was stored as 2023-03-02, "2023-06-15garbage" was accepted as 2023-06-15, and "25:70" was stored as 02:10 on the following day.

Both branches now switch lenient parsing off and parse through a ParsePosition, throwing the ParseException the method already declares unless the whole string is consumed. This matches the project's own OpenmrsDateFormat, which already defaults to non-lenient parsing. The same root cause in HL7Util is being fixed separately under TRUNK-6804, which does not cover these branches in Obs.

The second commit adds tests to ObsTest for the DT and TM branches: the valid values, and the invalid ones above now rejected with a ParseException.

I verified the change with a harness calling the real compiled api classes (javac, UTC): the three invalid inputs above now throw ParseException, and the controls DT "2023-06-15" and TM "13:45" store exactly the same values as before the change.

One honest note: I could not run the Maven build in my environment because it cannot download the project dependencies, so the module test suite has not been executed yet and CI will be the first real run.

## Issue I worked on

see https://issues.openmrs.org/browse/TRUNK-6848

## Checklist: I completed these to help reviewers :)

- [ ] My IDE is configured to follow the code style of this project.
- [x] I have added tests to cover my changes.
- [ ] I ran `./mvnw clean package` right before creating this pull request and added all formatting changes to my commit.
- [ ] All new and existing tests passed.
- [x] My pull request is based on the latest changes of the master branch.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2639edae597d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.