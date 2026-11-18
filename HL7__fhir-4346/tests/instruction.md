# Issue

**Title:** FHIR-56428: Rename MedicationDispense.notPerformedReason to statusReason

## Description

Resolves [FHIR-56428](https://jira.hl7.org/browse/FHIR-56428): MedicationDispense.notPerformedReason - should support more status changes

## What changed
Renamed MedicationDispense.notPerformedReason to statusReason, as in the Event pattern. Short "Reason for current status"; definition "Captures the reason for the current status of the dispense, for example why it was not performed, put on hold, or resumed." Type (CodeableReference(DetectedIssue)), cardinality (0..1) and the example binding to medicationdispense-status-reason are unchanged. Added the workflow mapping to Event.statusReason; the build regenerated the event mapping exceptions accordingly (statusReason is now a divergent element instead of unmapped).

Added three codes to the MedicationDispense Status Reason code system: on-hold ("Put on hold"), awaiting-authorization ("Awaiting authorization or payment") and issue-resolved ("Issue resolved", for a resumed dispense). The code system and value set descriptions now mention not performed, on-hold and resume.

fhir.ini: R5 to R6 map MedicationDispense.notPerformedReason -> statusReason; R4 to R6 map MedicationDispense.statusReason[x] -> statusReason. Examples medicationdispense0303, 0334 and 0335 and the UML diagram use the new name. Release note under "Changes since 6.0.0-ballot5", also covering FHIR-54366 (no restriction on which statuses can have a reason).

The resolution applies the rename if FMG has no objections: **FMG has no issues with the rename (2026-10-14).**

Master merged in (b0d2786389): the only conflict was the MedicationDispense release-note list (FHIR-59568), resolved by keeping both entries. Build after the merge: Summary Errors=0; statusReason, the mdd-1 of FHIR-59568 and both release notes are published.

Note: [FHIR-59520](https://jira.hl7.org/browse/FHIR-59520) (proposed, not yet voted) gives further details for this element (other status reason codes, definition and comment); it will be applied separately after its vote.

Build: Summary Errors=0 (full build); rebuild after adding the workflow mapping also Errors=0. Published output checked: statusReason definition and binding, the three new codes, the examples (no notPerformedReason left), release note, and "Renamed from notPerformedReason to statusReason" in the version comparison.

## Files touched
- `source/fhir.ini`
- `source/medicationdispense/codesystem-medicationdispense-status-reason.xml`
- `source/medicationdispense/medicationdispense-event-mapping-exceptions.xml`
- `source/medicationdispense/medicationdispense-introduction.xml`
- `source/medicationdispense/medicationdispense.svg`
- `source/medicationdispense/medicationdispense0303.xml`
- `source/medicationdispense/medicationdispense0334.xml`
- `source/medicationdispense/medicationdispense0335.xml`
- `source/medicationdispense/structuredefinition-MedicationDispense.xml`
- `source/medicationdispense/valueset-medicationdispense-status-reason.xml`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `12edb9a5ce0e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.