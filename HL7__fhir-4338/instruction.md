# Issue

**Title:** FHIR-54252: Add repeatCycle to DosageDetails (DosageInstruction)

## Description

## Summary

[FHIR-54252](https://jira.hl7.org/browse/FHIR-54252) – Adding a Repeat cycle element to DosageDetails (Persuasive with Modification, voted 20 May 2026, 12-1-2):
> Add repeatCycle (Duration) to DosageInstruction 0..1. Add at least one example. Add narrative explaining the limitations.

The minutes add "Leave all else as-is"; repeating at step level is for a separate ticket. DosageInstruction is the current DosageDetails (renamed by FHIR-54340, not yet applied).

## Changes

- `source/datatypes/dosagedetails.xml`: new element `DosageDetails.repeatCycle` (0..1, Duration), after `renderedInstruction`.
  - **Short:** "Repeat the dosage course after this duration".
  - **Definition:** the duration after which the whole dosage course (all its steps) starts again, measured from the start of the course.
  - **Comment:** the time after the last step until the end of the cycle is a period without doses; links to the limitations.
- `source/dosage.html`:
  - `repeatCycle` added to the DosageDetails summary list;
  - new section **Repeating cycles** (`#repeatcycle`) with the limitations:
    - it repeats the whole course, not a single step (`step.count` repeats a step);
    - the cycle is expected to be at least as long as the steps;
    - it does not say how many cycles or when to stop;
    - placebo days are a step with a dose, not days off.
- `source/dosage-examples.html`, Example 5 (21 days on, 7 days off):
  - structure list, YAML, JSON and XML use `repeatCycle` = 28 d with one step, once daily, bounded to 21 days;
  - this replaces the `endOffset` / frequency 21 per 28 days workaround;
  - title and notes unchanged.
- Release note in a new "Changes since 6.0.0-ballot5" block on `dosage.html`.

## QA

- Local build: `Summary: Errors=0` (full build); fragments checked, no errors.
- Generated `dosage-definitions.html`: `DosageDetails.repeatCycle`, 0..1 Duration, with short, definition and comment. Generated `dosagedetails.profile.json` has the element.
- Generated `dosage.html`: new section and release note. `dosage-examples.html` Example 5: no `endOffset` left.
- Build drift not related to this ticket (questionnaire/procedure mapping exceptions, spelling, snomed) was not committed.

## Related

- [FHIR-58720](https://jira.hl7.org/browse/FHIR-58720) (repeatCycle missing) and [FHIR-52901](https://jira.hl7.org/browse/FHIR-52901) (cyclical schedules) are on the Dosage Meeting A agenda and refer to this change.
- Also edits `dosage-examples.html`, like #4327 (Example 4), #4335 (contractions) and #4336 (Example 1), in different places.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cd042ebe5c72`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.