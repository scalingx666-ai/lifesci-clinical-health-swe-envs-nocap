# Issue

**Title:** Apply ServiceRequest example and scope clarifications

## Description

This PR addresses 4 tickets.

## Tickets

- [FHIR-58295](https://jira.hl7.org/browse/FHIR-58295): Add-on Example - should that have a link to the original ServiceRequest
- [FHIR-58294](https://jira.hl7.org/browse/FHIR-58294): Glucose example seems to be missing ServiceRequest.code
- [FHIR-58293](https://jira.hl7.org/browse/FHIR-58293): Add LOINC to Lipid Panel order example
- [FHIR-58287](https://jira.hl7.org/browse/FHIR-58287): Update "procedure" to "service" to avoid confusion

## FHIR-58295: Link the reflex order to its triggering request

Added a contained TSH ServiceRequest to the Free T4 example and linked the reflex order to it with `basedOn`. The self-contained reference avoids a broken published link while clearly showing the original order that initiated the reflex.

**Files:** `source/servicerequest/servicerequest-example-ft4.xml`, `source/servicerequest/servicerequest-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-58295)

---

## FHIR-58294: Add a code to the glucose request

Added LOINC `2345-7` and its standard display to the glucose ServiceRequest example, with concise concept text identifying the glucose test.

**Files:** `source/servicerequest/servicerequest-example-glucose.xml`, `source/servicerequest/servicerequest-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-58294)

---

## FHIR-58293: Add the standard lipid panel coding

Added LOINC `100898-6` and its standard display alongside the existing local lipid panel coding. The coding uses the canonical FHIR LOINC system URI, `http://loinc.org`.

**Files:** `source/servicerequest/servicerequest-example-lipid.xml`, `source/servicerequest/servicerequest-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-58293)

---

## FHIR-58287: Clarify the single-code scope

Replaced the procedure-based scope sentence with the approved single-code wording. The surrounding guidance for linking multiple ServiceRequests and using the Request pattern remains unchanged.

**Files:** `source/servicerequest/servicerequest-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-58287)

---

## Publisher QA

Final command: `./gradlew clean publish`

| metric | baseline | current | delta |
|---|---:|---:|---:|
| errors | 0 | 0 | 0 |
| warnings | 3752 | 3752 | 0 |
| info | 374 | 374 | 0 |
| broken_links | 0 | 0 | 0 |

## Published-output acceptance QA

| ticket | generated specification check |
|---|---|
| FHIR-58295 | The Free T4 narrative renders `basedOn` as a working link to the contained TSH original order; the TSH request renders LOINC `3016-3`; no broken/red reference remains. |
| FHIR-58294 | The glucose narrative renders “Glucose test” with LOINC `2345-7`, and the XML rendering includes the standard display. |
| FHIR-58293 | The lipid narrative renders both `{http://acme.org/tests LIPID}` and `{http://loinc.org 100898-6}`; the XML rendering includes “Lipid panel - Serum or Plasma”. |
| FHIR-58287 | The Scope and Usage page contains the approved “single code” wording, omits the replaced “single procedure” sentence, and preserves the adjacent Request-pattern guidance. |

The ServiceRequest “Changes since 6.0.0-ballot5” block renders one entry for each ticket.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1ff6826166d6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.