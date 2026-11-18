# Issue

**Title:** FHIR-49864: MedicationDispense example with a contained MedicationRequest

## Description

## Summary

[FHIR-49864](https://jira.hl7.org/browse/FHIR-49864) – MedicationDispense :: add new data elements - numberOfRepeats and numberDispensed (Persuasive with Modification, 5-0-0):
> The spec will be updated with an example using a contained MedicationRequest within the MedicationDispense. Number of dispenses already exists in the most current FHIR version in the fillNumber element, and so no change is required for this aspect of the request.

## Changes

- New example `medicationdispense0337` (`meddisp0337`), based on the ticket's use case (aged-care transfer, Pulmicort with 5 repeats):
  - contained MedicationRequest `#rx`: active order, Pulmicort Turbuhaler 400 microgram/actuation (budesonide), 1 inhalation twice daily, `dispenseRequest.numberOfRepeatsAllowed` = 5, 1 inhaler;
  - `authorizingPrescription` = `#rx`;
  - status completed, type v3-ActCode `RF` (Refill), 1 inhaler, daysSupply 30 days, `fillNumber` = 3, with a note: the original supply and the 2nd of the 5 repeats; 3 repeats remain.
- Entry in `list-MedicationDispense-examples.xml`.
- Release note in a new "Changes since 6.0.0-ballot5" block in `medicationdispense-introduction.xml`.

## QA

- Local build: `Summary: Errors=0`; the example validates, with no messages in the QA report.
- Generated `medicationdispense0337.html` shows the dispense and the contained prescription, including the number of repeats allowed. The example is listed on the examples page; the release note is shown on `medicationdispense.html`.

## Note on merging

#4328 and #4331 also create the "Changes since 6.0.0-ballot5" block in `medicationdispense-introduction.xml`. Whichever merges later needs a small merge to combine the list items.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cd042ebe5c72`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.