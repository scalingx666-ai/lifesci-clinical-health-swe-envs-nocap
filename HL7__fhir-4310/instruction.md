# Issue

**Title:** FHIR-58252/58255/58467/12913: Update Specimen and Diagnostics

## Description

## HL7 FHIR Pull Request

_Note: No pull requests will be accepted against `./source` unless logged in the_ [HL7 Jira issue tracker](https://jira.hl7.org/projects/FHIR/issues/).

Jira tracker numbers: `FHIR-58252`, `FHIR-58255`, `FHIR-58467`, `FHIR-12913`

## Description

This PR addresses four resolved tickets across Specimen and the Diagnostics Module. Each ticket has its own commit and an entry under **Changes since 6.0.0-ballot5** on the affected page; the historical Ballot5 notes are unchanged.

## Tickets

- [FHIR-58252](https://jira.hl7.org/browse/FHIR-58252): Do we need to add a search parameter for .focus?
- [FHIR-58255](https://jira.hl7.org/browse/FHIR-58255): Update example Liver biopsy specimen (id = "liver-biopsy")
- [FHIR-58467](https://jira.hl7.org/browse/FHIR-58467): Consider allowing Organization and HealthcareService as Specimen.processing.performer targets.
- [FHIR-12913](https://jira.hl7.org/browse/FHIR-12913): Create a profile for "Patient characteristics"

## FHIR-58252: Do we need to add a search parameter for .focus?

Added a focus reference search parameter for Specimen.focus and documented it under Changes since 6.0.0-ballot5 on the Specimen resource page. The current element is a Reference, so a single reference search parameter is appropriate.

**Files:** `source/specimen/bundle-Specimen-search-params.xml`, `source/specimen/specimen-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-58252)

---

## FHIR-58255: Update example Liver biopsy specimen (id = "liver-biopsy")

Updated the liver-biopsy Specimen to reference a contained order for surgical pathology testing, use the liver-specific tissue type, and identify its collection method with SNOMED CT `287489008` (Percutaneous needle biopsy of liver). Corrected an initial wrong-code/display pairing after CI reported that `62438007` means pancreas transplantation. Documented the example change under Changes since 6.0.0-ballot5 on the Specimen resource page.

**Files:** `source/specimen/specimen-example-liver-biopsy.xml`, `source/specimen/specimen-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-58255)

---

## FHIR-58467: Consider allowing Organization and HealthcareService as Specimen.processing.performer targets.

Added Organization as a permitted reference target for Specimen.processing.performer and documented the change under Changes since 6.0.0-ballot5 on the Specimen resource page. HealthcareService remains excluded, as specified by the modified disposition.

**Files:** `source/specimen/structuredefinition-Specimen.xml`, `source/specimen/specimen-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-58467)

---

## FHIR-12913: Create a profile for "Patient characteristics"

Added a patient-characteristics roadmap bullet to the Diagnostics Module, linking PSS-2205 and the balloted AIPC logical model, and documented the addition under Changes since 6.0.0-ballot5. No Observation profile was created because the modified disposition calls only for roadmap guidance.

**Files:** `source/diagnostics-module.html`

[Ticket](https://jira.hl7.org/browse/FHIR-12913)

---

## Publisher QA

The current branch's full `./gradlew publish` completed successfully with **0 errors, 83 warnings, and 624 hints**. The generated liver-biopsy XML and HTML both show SNOMED CT `287489008` with the intended display. HL7's live terminology server accepted the exact code/display pair using `$validate-code`. The affected resource pages show the release notes under **Changes since 6.0.0-ballot5**.

The counts above are from the post-merge branch. Earlier baseline/branch validation counts (0 errors, 80 warnings, 347 hints) were obtained before a subsequent upstream merge and are not directly comparable to this build. The installed QA parser expects a different summary-line format, so these counts were transcribed from publisher logs. Broken-link totals were not measured by that summary.

The liver-biopsy example's existing `Practitioner/gastroenterologist` collector reference still renders as a broken link; this PR resolves the separate `Specimen.request` link identified by FHIR-58255. The AIPC PDF URL matches the accepted JIRA resolution, but its live availability could not be confirmed by the automated request (the document server returned HTTP 202 without content). FHIR-58256, which updates the collection-method value set, is a separate ticket and is not implemented here.

Draft PR #4309 also edits `source/specimen/specimen-example-liver-biopsy.xml` and `source/specimen/specimen-introduction.xml`; whichever PR merges second may need conflict resolution.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ef782bfa3e71`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.