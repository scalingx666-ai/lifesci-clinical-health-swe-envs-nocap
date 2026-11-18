# Issue

**Title:** FHIR-45330, FHIR-45329, FHIR-33986: Medical gas, device and catheter port examples

## Description

## Summary

Three related example tickets in one PR, because the examples reference each other. There is one commit per ticket, plus two review iterations on FHIR-45330.

- [FHIR-45330](https://jira.hl7.org/browse/FHIR-45330) – Add medical gas orders examples to MedicationRequest (Persuasive, 5-0-0): "We will create the examples using the information provided."
- [FHIR-45329](https://jira.hl7.org/browse/FHIR-45329) – Include example of MedicationRequest, etc. involving Device (Persuasive, 5-0-0): an example MedicationRequest referencing a DeviceDefinition, and a MedicationAdministration referencing a Device.
- [FHIR-33986](https://jira.hl7.org/browse/FHIR-33986) – Administered via distal port in a triple lumen catheter (Persuasive, 4-0-0): an example with a Device reference from the MedicationAdministration for the port, and the parent Device for the triple lumen catheter.

## Examples

- **medicationrequest0351 (FHIR-45330):**
  - HeliOx 79/21, SNOMED CT 895694008 "Helium 0.79 mL/mL and oxygen 0.21 mL/mL gas for inhalation";
  - 6 to 8 L/min (`rateRange`) via non-rebreather mask (device concept, SNOMED CT 427591007);
  - reason croup.
- **medicationrequest0352 (FHIR-45330, FHIR-45329):**
  - supplementary oxygen (SNOMED CT 320917000), 1 to 3 L/min;
  - `asNeededFor` SpO2 below 88% (SNOMED CT 449171008);
  - via nasal cannula: a **contained DeviceDefinition** referenced from `MedicationRequest.device`;
  - same `groupIdentifier` as 0351.
- **medicationadministration0314 (FHIR-33986, FHIR-45329):**
  - vancomycin 1 g IV, by infusion pump, through the distal port of a triple lumen catheter;
  - `MedicationAdministration.device` references the contained port Device (with `parent` = the contained catheter Device, SNOMED CT 397970004) and the contained infusion pump Device (SNOMED CT 430033006).

The devices are contained in the Medication examples, rather than added as separate Device/DeviceDefinition examples in the Orders & Observations folders. Each example has an entry in its examples list. Release notes are under "Changes since 6.0.0-ballot5" in the MedicationRequest and MedicationAdministration introductions.

## QA

- Local build: `Summary: Errors=0`. The first build caught the missing `DeviceDefinition.status`, which is fixed in a separate commit. The three examples validate with no messages in the QA report and render with the contained devices.
- Review iteration: HeliOx changed from 70/30 (895532000) to 79/21 (895694008), as in the resolution.
- Build drift not related to these tickets (procedure mapping exceptions, loinc, snomed) was not committed.

## Follow-up

[FHIR-45331](https://jira.hl7.org/browse/FHIR-45331): inform O&O about these examples once merged.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cd042ebe5c72`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.