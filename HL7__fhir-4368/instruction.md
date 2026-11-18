# Issue

**Title:** FHIR-58643: Remove MedicationRequest.isRecordOfRequest

## Description

Resolves [FHIR-58643](https://jira.hl7.org/browse/FHIR-58643): MedicationRequest.isRecordOfRequest needs to be dropped (Persuasive, voted 2026-10-19).

Also resolves, with the same change: [FHIR-53305](https://jira.hl7.org/browse/FHIR-53305), [FHIR-54446](https://jira.hl7.org/browse/FHIR-54446), [FHIR-58459](https://jira.hl7.org/browse/FHIR-58459), [FHIR-55006](https://jira.hl7.org/browse/FHIR-55006) ("the element will be removed as per FHIR-58643"). Makes [FHIR-49863](https://jira.hl7.org/browse/FHIR-49863) (rename to isRecordOfRequest) and [FHIR-55005](https://jira.hl7.org/browse/FHIR-55005) (element position) moot.

## What changed
- Removed `MedicationRequest.isRecordOfRequest` (R5 `MedicationRequest.reported`).
- Scope and Usage: after "… see Workflow Request" added: "– it serves as an authorization, which doesn't make it necessarily actionable, unless it has the 'actionable' tag set, or used in combination with a Task resource or in specific workflows - more information on the [workflow pages](workflow-management.html)."
- `informationSource`: removed the definition sentence that referred to `.isRecordOfRequest`, and the reference to it in the comment.
- `fhir.ini`: R4 `reported[x]` and R5 `reported` mapped as removed (FHIR-58643).
- Release note under "Changes since 6.0.0-ballot5".
- Removed the `isRecordOfRequest` line from two files that are not built: `medicationrequest0340.xml` (not in the example list; also fixes its broken XML) and the stale `medicationadministration/immunization-example-refused.xml`.

## Build
Summary Errors=0. The element is not in the profile or the definitions; the guidance and the release note are on medicationrequest.html; the version comparison shows `reported` as removed.

Note: #4347 (FHIR-54340) also adds an entry to the MedicationRequest release-note list – a small merge for whichever is merged later.

Disposition: Persuasive

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b4ace6735385`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.