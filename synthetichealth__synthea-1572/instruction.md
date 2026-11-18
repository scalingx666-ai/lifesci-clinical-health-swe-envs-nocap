# Issue

**Title:** Set MedicationRequest status to COMPLETE instead of STOPPED

## Description

This PR fixes a discrepancy in how MedicationRequests are created by the synthea R4 export. The previous code was setting the MedicationRequest to STOPPED if the medication has a valid stop value. But looking at the [MedicationRequest status valueset](https://hl7.org/fhir/R4/valueset-medicationrequest-status.html), stopped means:

> Actions implied by the prescription are to be permanently halted, before all of the administrations occurred. This should not be used if the original order was entered in error

Essentially this seems to mean that the request was stopped rather than that the medication itself was stopped. For most synthea modules, the intent is for medication.stop to get set to something other than 0L when the medication is _completed_. As such, we want to set the MedicationRequest to COMPLETED for this case to capture the intent of those modules.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bdc91c0d3525`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.