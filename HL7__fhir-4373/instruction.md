# Issue

**Title:** Add BodyStructure predecessors and examples; clarify ServiceRequest

## Description

Adds BodyStructure predecessor relationships and six examples, clarifies the ServiceRequest procedure workflow, and records FHIR-58612 alongside the existing morphology change note. The batch has four commits for work still needed; FHIR-57353 was already implemented in merged PR #4367 and was verified against its current resolution.

Both resource pages record the changes under **Changes since 6.0.0-ballot5**. The historical ballot notes are unchanged.

## Tickets

- [FHIR-58286](https://jira.hl7.org/browse/FHIR-58286): Clarify that the procedure workflow is an example
- [FHIR-58612](https://jira.hl7.org/browse/FHIR-58612): Attribute the existing overall morphology change
- [FHIR-57384](https://jira.hl7.org/browse/FHIR-57384): Add BodyStructure predecessor relationships
- [FHIR-59662](https://jira.hl7.org/browse/FHIR-59662): Add morphology examples
- [FHIR-57353](https://jira.hl7.org/browse/FHIR-57353): Verify the previously merged morphology implementation

## FHIR-58286: Procedure workflow as an example

Added the approved procedure-example qualifier to the ServiceRequest Scope and Usage paragraph, preserved its remaining sentences, and recorded the clarification under Changes since 6.0.0-ballot5.

**Files:** `source/servicerequest/servicerequest-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-58286)

---

## FHIR-58612: Allow .morphology at the top level of BodyStructure

Added FHIR-58612 to the existing BodyStructure morphology change note. The model change was already implemented through FHIR-57353 in merged PR #4367, and its current definition, cardinality, datatype, binding, and summary flag were verified.

**Files:** `source/bodystructure/bodystructure-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-58612)

---

## FHIR-57384: BodyStructure predecessor relationships

Added BodyStructure.predecessor as 0..* CodeableReference(BodyStructure), with the approved definition and directional relationship comment, example body-site binding, and reference and token search parameters. Added the three supplied liver-neoplasm examples with preserved tracking identifiers and correctly nested predecessor references, explanatory guidance, example registrations, and a resource-page release note.

The implementation uses the explicitly specified CodeableReference datatype in the disposition. The supplied examples' plain reference values were wrapped to match that datatype, as approved in the batch plan.

**Files:** `source/bodystructure/structuredefinition-BodyStructure.xml`, `source/bodystructure/bundle-BodyStructure-search-params.xml`, `source/bodystructure/bodystructure-introduction.xml`, `source/bodystructure/list-BodyStructure-examples.xml`, `source/bodystructure/bodystructure-example-liver-neoplasm1.xml`, `source/bodystructure/bodystructure-example-liver-neoplasm2.xml`, `source/bodystructure/bodystructure-example-liver-neoplasm3.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-57384)

---

## FHIR-59662: Morphology examples

Added the supplied cardiac-myxoma, right-lung-consolidation, and aortic-dissection examples as XML with explanatory narratives, registered example links, and a resource-page release note. Preserved the submitted codes with terminology-server-validated displays; the lung example includes its lower-lobe exclusion and the aortic example retains both overall and per-structure morphology.

**Files:** `source/bodystructure/bodystructure-example-cardiac-myxoma.xml`, `source/bodystructure/bodystructure-example-right-lung-consolidation.xml`, `source/bodystructure/bodystructure-example-aortic-dissection.xml`, `source/bodystructure/list-BodyStructure-examples.xml`, `source/bodystructure/bodystructure-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-59662)

---

## FHIR-57353: Morphologies spanning multiple BodyStructure.includedStructures

Verified that the implementation already merged in PR #4367 matches the current resolution, including the full definition and comment passages, cardinalities, bindings, summary flags, and morphology search expression. No new model change or implementation commit was needed for this ticket.

[Ticket](https://jira.hl7.org/browse/FHIR-57353)

---

## Publisher QA

The full publisher completed successfully on the batch branch with `./gradlew publish --args="-nopartial -nosound"`. The baseline was a successful full build of unmodified master at `c6d21e0342`.

| metric | baseline | current | delta |
|---|---:|---:|---:|
| errors | 0 | 0 | 0 |
| warnings | 3751 | 3757 | +6 |
| info | 384 | 384 | 0 |
| external Extensions link reports | 3 | 3 | 0 |

All 70 semantic checks passed across the five trackers, with a separate local QA record for each ticket. Checks covered complete approved passages, generated definitions and XSD, search parameters and registry entries, all six example XML/JSON/narrative outputs, preserved tracking identifiers, predecessor reference nesting, and unique release-note placement. The rendered narratives and predecessor links were also inspected in Chrome. All supplied SNOMED CT, RadLex, and DICOM codes and displays passed validation against tx.fhir.org.

The six additional instance warnings are two per liver-neoplasm example: the supplied DICOM Tracking Identifier (112039) and Tracking Unique Identifier (112040) codes are outside the extensibly bound FHIR Identifier Type Codes value set. Their codes and identifier values are preserved. Separately, the content-quality report warns that the exact approved predecessor short description repeats the element name, and notes that the supplied examples do not exercise predecessor.concept. The agreed wording and examples are retained.

The same three external Extensions links are reported in baseline and final builds: timing-dayOfMonth, domainresource, and DeviceAlert.

## Publisher-generated source updates

The publisher regenerated `source/questionnaire/questionnaire-fivews-mapping-exceptions.xml` and added `lifecycle`, `subject_state`, and `hrf` to `source/spelling/add.txt`. Those tracked changes are retained with the ticket edits, as required by the batch workflow. Generated site files and local QA caches are excluded from the PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c6d21e0342f4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.