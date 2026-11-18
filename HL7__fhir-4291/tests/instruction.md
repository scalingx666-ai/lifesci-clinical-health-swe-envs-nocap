# Issue

**Title:** Apply remaining OO clarifications and SampledData examples

## Description

This PR implements the seven remaining tickets from a 12-ticket batch and records the resource-page ballot impact of all 12 tickets.

## Requested batch context

The original batch contained 12 tickets. [FHIR-58530](https://jira.hl7.org/browse/FHIR-58530) was already merged in , while [FHIR-58295](https://jira.hl7.org/browse/FHIR-58295), [FHIR-58294](https://jira.hl7.org/browse/FHIR-58294), [FHIR-58293](https://jira.hl7.org/browse/FHIR-58293), and [FHIR-58287](https://jira.hl7.org/browse/FHIR-58287) were already merged in . This PR contains the seven remaining implementations without duplicating the five completed changes. It also adds the impact of all 12 tickets to the existing categorized `Note to Balloters for Ballot5` on the affected resource pages.

## Resource-page ballot impact

- **Compatible substantive:** FHIR-58530 on ServiceRequest.
- **Non-substantive:** FHIR-58416 on Specimen; FHIR-58415, FHIR-57931, and FHIR-57930 on BodyStructure; FHIR-58295, FHIR-58294, FHIR-58293, FHIR-58291, FHIR-58290, and FHIR-58287 on ServiceRequest; and FHIR-24662 on Observation.
- Updated each resource note's opening impact summary where needed and retained its relevant module-page cross-reference: Diagnostics for all four resources, plus Workflow for ServiceRequest.
- Integrated each ticket into the existing categorized ballot note rather than adding a parallel changes-since note.

## Tickets
- [FHIR-58416](https://jira.hl7.org/browse/FHIR-58416): Specimen.collection.fastingStatus has minor typos
- [FHIR-58415](https://jira.hl7.org/browse/FHIR-58415): Definition of BodyStructure.includedStructure.morphology references an element that was removed in R5
- [FHIR-58291](https://jira.hl7.org/browse/FHIR-58291): Clarify the definition fo ServiceRequest.subject
- [FHIR-58290](https://jira.hl7.org/browse/FHIR-58290): Add to comment, that for lab tests the binding for .code should be LOINC or a SCT from the observablehierarchy
- [FHIR-57931](https://jira.hl7.org/browse/FHIR-57931): Rephrase definition for more clarity
- [FHIR-57930](https://jira.hl7.org/browse/FHIR-57930): Typo at the definition of BodyStructure.includedStructure.bodyLandmarkOrientation.clockFacePosition
- [FHIR-24662](https://jira.hl7.org/browse/FHIR-24662): Add means to allow an annotation to a sample in SampledData

## FHIR-58416: Specimen.collection.fastingStatus has minor typos

Corrected the Specimen.collection.fastingStatus[x] comment so the component reference is rendered as Observation.component.code without the stray backtick, and recorded the correction as non-substantive in the Specimen ballot note.

**Files:** `source/specimen/structuredefinition-Specimen.xml`, `source/specimen/specimen-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-58416)

---

## FHIR-58415: Definition of BodyStructure.includedStructure.morphology references an element that was removed in R5

Replaced the BodyStructure.includedStructure.morphology definition with the approved wording describing the included anatomical or pathological structure, removing the obsolete BodyStructure.location reference. Recorded the correction as non-substantive in the BodyStructure ballot note.

**Files:** `source/bodystructure/structuredefinition-BodyStructure.xml`, `source/bodystructure/bodystructure-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-58415)

---

## FHIR-58291: Clarify the definition fo ServiceRequest.subject

Clarified ServiceRequest.subject to distinguish the individual or entity of record from the target of the requested service. The short description and definition now describe whose or what record holds the service request, while retaining the existing examples of supported subject types. Recorded the change as non-substantive in the ServiceRequest ballot note.

**Files:** `source/servicerequest/structuredefinition-ServiceRequest.xml`, `source/servicerequest/servicerequest-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-58291)

---

## FHIR-58290: Add to comment, that for lab tests the binding for .code should be LOINC or a SCT from the observablehierarchy

Added terminology guidance to ServiceRequest.code for laboratory tests and radiology. The comment now directs authors to LOINC or the SNOMED CT Observable Entity hierarchy, while retaining the existing guidance about codes that include specimen or organ-system context and the use of PlanDefinition for grouped activities. Recorded the change as non-substantive in the ServiceRequest ballot note.

**Files:** `source/servicerequest/structuredefinition-ServiceRequest.xml`, `source/servicerequest/servicerequest-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-58290)

---

## FHIR-57931: Rephrase definition for more clarity

Clarified the BodyStructure landmarkDescription definition. The revised wording states that the body landmark description locates the corresponding structure rather than the vague phrase “something else.” Recorded the change as non-substantive in the BodyStructure ballot note.

**Files:** `source/bodystructure/structuredefinition-BodyStructure.xml`, `source/bodystructure/bodystructure-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-57931)

---

## FHIR-57930: Typo at the definition of BodyStructure.includedStructure.bodyLandmarkOrientation.clockFacePosition

Corrected the grammatical typo in the BodyStructure clockFacePosition definition by changing “An description” to “A description.” Recorded the change as non-substantive in the BodyStructure ballot note.

**Files:** `source/bodystructure/structuredefinition-BodyStructure.xml`, `source/bodystructure/bodystructure-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-57930)

---

## FHIR-24662: Add means to allow an annotation to a sample in SampledData

Added two paired-Observation examples showing how to annotate samples in an existing EKG SampledData Observation without changing the SampledData structure. One example identifies an abnormal interval with valuePeriod. The other uses coded SampledData and a contained ConceptMap to map per-sample SNOMED CT rhythm codes to LOINC answer codes. Both derive from the existing Observation/ekg example and are registered in the Observation example list and Device Generated Data section. Recorded the change as non-substantive in the Observation ballot note.

**Files:** `source/observation/observation-example-ekg-abnormal-period.xml`, `source/observation/observation-example-ekg-coded-annotations.xml`, `source/observation/list-Observation-examples.xml`, `source/observation/observation-examples-header.xml`, `source/observation/observation-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-24662)

---

## Publisher QA

| metric | baseline | current | delta |
|---|---:|---:|---:|
| errors | 1 | 1 | 0 |
| warnings | 3753 | 3754 | +1 |
| info | 373 | 374 | +1 |
| broken_links | 0 | 0 | 0 |

The sole publisher error is unchanged from the baseline and is the existing terminology validation failure in `riskassessment-example-prognosis`. None of the edited resources introduced a new error or broken link. Both new Observation examples passed instance validation. Generated-output checks passed for the seven implemented tickets, and the Specimen, BodyStructure, ServiceRequest, and Observation main resource pages were verified to contain each of the 12 requested JIRA links exactly once under the intended impact category, with their module-page cross-references intact.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dfc3ff074ad6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.