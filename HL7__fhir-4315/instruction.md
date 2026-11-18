# Issue

**Title:** Resolve six OO FHIR trackers across BodyStructure, search, and DiagnosticReport

## Description

This PR addresses 6 ticket(s).

## Tickets
- [FHIR-57929](https://jira.hl7.org/browse/FHIR-57929): Current structure allows to create a contradicting resource
- [FHIR-57928](https://jira.hl7.org/browse/FHIR-57928): No example for ExcludedStructure available
- [FHIR-59412](https://jira.hl7.org/browse/FHIR-59412): Change bodyStructure search parameter in Specimen
- [FHIR-58061](https://jira.hl7.org/browse/FHIR-58061): SearchParameter name from 'reference' to 'body-structure-reference'
- [FHIR-58062](https://jira.hl7.org/browse/FHIR-58062): SearchParameter name from 'reference' to 'body-structure-reference'
- [FHIR-58360](https://jira.hl7.org/browse/FHIR-58360): Clarification about boundaries between DiagnosticReport and Procedure

## FHIR-57929: Current structure allows to create a contradicting resource

Added comments to the BodyStructure includedStructure and excludedStructure definitions to clarify that the same fully specified anatomical area should not be both included and excluded. Recorded the change under Changes since 6.0.0-ballot5. The publisher also refreshed tracked Questionnaire Five Ws mapping exceptions and the spelling additions list; these cross-resource updates are included in this commit as required by the workflow.

**Files:** `source/bodystructure/structuredefinition-BodyStructure.xml`, `source/bodystructure/bodystructure-introduction.xml`, `source/questionnaire/questionnaire-fivews-mapping-exceptions.xml`, `source/spelling/add.txt`

[Ticket](https://jira.hl7.org/browse/FHIR-57929)

---

## FHIR-57928: No example for ExcludedStructure available

Added a dermatology BodyStructure example that includes facial skin but excludes eyelid skin, and listed it on the BodyStructure examples page with a human-readable description. Recorded the example under Changes since 6.0.0-ballot5.

**Files:** `source/bodystructure/bodystructure-example-face-excluding-eyelids.xml`, `source/bodystructure/list-BodyStructure-examples.xml`, `source/bodystructure/bodystructure-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-57928)

---

## FHIR-59412: Change bodyStructure search parameter in Specimen

Renamed the Specimen collection body-structure reference search parameter's id, canonical URL, and code to body-structure-reference while retaining its reference expression. Recorded the change under Changes since 6.0.0-ballot5 on the Specimen resource page.

**Files:** `source/specimen/bundle-Specimen-search-params.xml`, `source/specimen/specimen-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-59412)

---

## FHIR-58061: SearchParameter name from 'reference' to 'body-structure-reference'

Changed the ServiceRequest body-structure reference search parameter code from reference to body-structure-reference, leaving its existing id, canonical URL, target, and expression intact. Recorded the change under Changes since 6.0.0-ballot5 on the ServiceRequest resource page.

**Files:** `source/servicerequest/bundle-ServiceRequest-search-params.xml`, `source/servicerequest/servicerequest-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-58061)

---

## FHIR-58062: SearchParameter name from 'reference' to 'body-structure-reference'

Changed the Observation body-structure reference search parameter code from reference to body-structure-reference, leaving its existing id, canonical URL, target, and expression intact. Recorded the change under Changes since 6.0.0-ballot5 on the Observation resource page.

**Files:** `source/observation/bundle-Observation-search-params.xml`, `source/observation/observation-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-58062)

---

## FHIR-58360: Clarification about boundaries between DiagnosticReport and Procedure

Clarified DiagnosticReport's Boundaries and Relationships guidance to distinguish Procedure activity and effects from the findings of diagnostic evaluations, which belong in observations and reports. Added a linked entry under Changes since 6.0.0-ballot5 on the DiagnosticReport resource page.

**Files:** `source/diagnosticreport/diagnosticreport-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-58360)

---

## Publisher QA

The final local publisher run completed successfully with zero errors. Each of the six tickets also passed a separate check of its generated resource page and relevant definitions, search-parameter page, or example. Warning and information counts below come from incremental publisher runs and are not directly comparable with the clean baseline; their differences do not establish that those messages were resolved.

| metric | baseline | current | delta |
|---|---:|---:|---:|
| errors | 0 | 0 | 0 |
| warnings | 3825 | 2384 | -1441 |
| info | 385 | 161 | -224 |
| broken_links | 0 | 0 | 0 |

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3460f8d66b4e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.