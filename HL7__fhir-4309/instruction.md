# Issue

**Title:** FHIR-59011, FHIR-58904, FHIR-58512, FHIR-58465: Update Specimen

## Description

## HL7 FHIR Pull Request

Associated Jira trackers: [FHIR-59011](https://jira.hl7.org/browse/FHIR-59011), [FHIR-58904](https://jira.hl7.org/browse/FHIR-58904), [FHIR-58512](https://jira.hl7.org/browse/FHIR-58512), and [FHIR-58465](https://jira.hl7.org/browse/FHIR-58465).

## Description

Specimen now allows collection collector and procedure details to coexist when their performer information is consistent, describes its subject of record more precisely, and connects the liver-biopsy example to the Procedure that collected it. Each change is documented under **Changes since 6.0.0-ballot5**.

### Tickets

| Ticket | Result | JIRA impact |
|---|---|---|
| [FHIR-59011](https://jira.hl7.org/browse/FHIR-59011) | The liver-biopsy Specimen references a contained completed Procedure and retains its biopsy collection method. | Non-substantive |
| [FHIR-58904](https://jira.hl7.org/browse/FHIR-58904) | The collector/procedure mutual-exclusion rule is removed, and both elements explain the consistency expectation. | Compatible, substantive |
| [FHIR-58512](https://jira.hl7.org/browse/FHIR-58512) | The `Specimen.subject` short display now states that the specimen was obtained for the subject of record. | Non-substantive |
| [FHIR-58465](https://jira.hl7.org/browse/FHIR-58465) | The resource page records the linked collector/procedure resolution implemented by FHIR-58904. | Non-substantive |

FHIR-58465 points to FHIR-58904 for the model change. It therefore has a separate ticket commit and release-note entry, while the constraint removal and element guidance remain in the FHIR-58904 commit.

### Publisher QA

The current branch's full `./gradlew publish` completed successfully with **0 errors, 83 warnings, and 622 hints**. The generated liver-biopsy XML, JSON, and HTML show SNOMED CT `287489008` with the display “Percutaneous needle biopsy of liver” for the contained Procedure. HL7's live terminology server accepts that exact code/display pair. This corrects the former `62438007` pairing, which the terminology server identifies as pancreas transplantation.

Generated-output checks passed separately for all four tickets:

- the Specimen page contains one linked entry for each ticket under **Changes since 6.0.0-ballot5**;
- the `Specimen.subject` short display is updated in the definition page and generated XML and JSON;
- `spm-1` is absent, and the collector/procedure consistency guidance appears on both element definitions; and
- the rendered liver-biopsy example links its collection procedure to the contained Procedure and shows SNOMED CT codes `287489008` and `129314006`.

The counts above are from the post-merge branch. Earlier baseline/branch counts (0 errors, 80 warnings, 347 hints) came from before a subsequent upstream merge and are not directly comparable. The example's existing `ServiceRequest/liver-biopsy-request` and `Practitioner/gastroenterologist` references still render as broken links; this correction addresses only the procedure code/display mismatch.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0083a7902f3e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.