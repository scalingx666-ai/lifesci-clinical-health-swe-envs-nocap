# Issue

**Title:** FHIR-54340: Rename the DosageDetails data type to DosageInstruction

## Description

Resolves [FHIR-54340](https://jira.hl7.org/browse/FHIR-54340): Rename DosageDetails to InstructionsForUse

## What changed
Renames the R6 data type DosageDetails to DosageInstruction, as resolved
(12-1-0). The content of the type is unchanged.
- source/datatypes/dosagedetails.xml renamed to dosageinstruction.xml,
  with all element paths (DosageInstruction.renderedInstruction,
  .repeatCycle, .step..., .safety). Invariant keys dosdet-1/-2 kept.
- fhir.ini: type list, page, work group, standards status and invariant
  prefix entries renamed. The historical [removed-resources] and
  [r2-renames] entries for DosageInstruction are unchanged.
- Types of MedicationRequest.dosageInstruction,
  MedicationDispense.dosageInstruction, MedicationStatement.dosage and
  ActivityDefinition.dosageInstruction (CDS; a CDS ticket is being
  raised for agreement) changed to DosageInstruction.
- dosage.html, dosage-definitions.html, dosage-examples.html,
  specialtypes.diagram and the medication introductions updated; the
  dosage page keeps an extra #DosageDetails anchor for old links.
  history.html and datatypes/_changelog.txt keep the old name (history).
- Release notes under "Changes since 6.0.0-ballot5" on the Dosage page,
  MedicationRequest, MedicationDispense, MedicationStatement and
  ActivityDefinition.
The branch has master merged in (2c21af7bfd, no conflicts), including the Dosage typo fixes from #4344 and the Medication changes from #4339.

ActivityDefinition.dosageInstruction belongs to CDS: a ticket asking CDS to agree to the type change is drafted and will be linked here.

Build: Summary Errors=0 (full build, before and after the master merge); the generated profile is StructureDefinition/DosageInstruction and the four elements use it.

## Files touched
- `source/activitydefinition/activitydefinition-introduction.xml`
- `source/activitydefinition/structuredefinition-ActivityDefinition.xml`
- `source/datatypes/dosageinstruction.xml`
- `source/datatypes/specialtypes.diagram`
- `source/dosage-definitions.html`
- `source/dosage-examples.html`
- `source/dosage.html`
- `source/fhir.ini`
- `source/medicationdispense/medicationdispense-introduction.xml`
- `source/medicationdispense/structuredefinition-MedicationDispense.xml`
- `source/medicationrequest/medicationrequest-introduction.xml`
- `source/medicationrequest/structuredefinition-MedicationRequest.xml`
- `source/medicationstatement/medicationstatement-introduction.xml`
- `source/medicationstatement/structuredefinition-MedicationStatement.xml`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `946ad28ccf3f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.