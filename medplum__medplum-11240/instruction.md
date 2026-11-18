# Issue

**Title:** fix(core): display strings for Coverage, Immunization, and referenced medications

## Description

`getDisplayString` fell back to the reference string ("Coverage/123") for these, which is all a reviewer sees when records come from another system, such as a SMART Health Links or Check-in share.

- Coverage: the first payor display name, else the coverage type
- Immunization: vaccineCode
- MedicationRequest and MedicationStatement: after medicationCodeableConcept, the medicationReference display, then the code of a contained Medication ("#id")

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7af3916e25c7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.