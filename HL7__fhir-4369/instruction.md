# Issue

**Title:** FHIR-58128: 'No known medications' in the MedicationStatement definitions

## Description

Resolves [FHIR-58128](https://jira.hl7.org/browse/FHIR-58128): Describe "no known medications" in the definitions (Persuasive with Modification, voted 2026-10-19).

## What changed
- `MedicationStatement` (resource definition): added at the end "A MedicationStatement can also be used to state that the patient has no known medications (see Scope and Usage)."
- `MedicationStatement.medication` definition: "Identifies the medication taken (or not taken), or states that there are no known medications. This is either a link to a resource representing the details of the medication or a code that identifies the medication from a known list of medications, or a code such as SNOMED CT 787481004 |No known medications|."
- `MedicationStatement.medication` short: "The medication that is/was taken (or not taken), or no known medications".
- Release note under "Changes since 6.0.0-ballot5".
- The build updated the Event mapping exceptions with the new short and definition.

## Build
Summary Errors=0; the three texts and the release note are published; the old wording ("a simple attribute carrying a code") is gone.

Note: #4347 (FHIR-54340) also adds an entry to the MedicationStatement release-note list – a small merge for whichever is merged later.

Disposition: Persuasive with Modification

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b4ace6735385`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.