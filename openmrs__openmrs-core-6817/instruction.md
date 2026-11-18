# Issue

**Title:** TRUNK-6848: Revert "Reject invalid dates and times in Obs.setValueAsString for DT and TM datatypes" (2.8.x)

## Description

## Description of what I changed
Reverts 50de2713a (TRUNK-6848, #6732) on `2.8.x` while its behavior changes are reviewed:

1. **DT values with a time part.** The time used to be dropped and the value stored as midnight. ISO input with a `T` now keeps the time and offset, so DT obs can get a non-midnight `value_datetime`, and the stored date can change depending on the server's time zone.
2. **Previously accepted DT input is now rejected.** `yyyy-MM-dd HH:mm[:ss]` used to be accepted (time dropped) and is now a `ParseException`. This breaks existing clients, e.g. labtrackingapp, which sends that format for a DT concept and now gets a 400 saving specimen details. TS parsing is still lenient, so the method is now inconsistent across datatypes.

The intended fixes (rejecting `2023-02-30`, trailing garbage, `25:70`) are good. They can come back with the DT changes above addressed. Details on the ticket.

This is a plain `git revert` with no conflicts. One revert PR per branch: #6732 went to master and was backported to 2.9.x and 2.8.x. Tests: ObsTest passes locally (57 tests, 0 failures).

## Issue I worked on
see https://issues.openmrs.org/browse/TRUNK-6848

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f4675aba459d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.