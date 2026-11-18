# Issue

**Title:** FHIR-59524, FHIR-57429: Medication serial-number search; identifier vs instance.identifier with examples

## Description

This PR addresses 2 tickets (one commit each).

## Tickets
- [FHIR-59524](https://jira.hl7.org/browse/FHIR-59524): Medication search parameter serial-number should search Medication.instance.identifier
- [FHIR-57429](https://jira.hl7.org/browse/FHIR-57429): Clarify Medication.identifier vs Medication.instance.identifier

## FHIR-59524
In `source/medication/bundle-Medication-search-params.xml`:
- `serial-number`: expression and build path changed to `Medication.instance.identifier` (were `Medication.identifier` / `Medication.instance.lotNumber`). Description (from FHIR-54379) unchanged.
- `lot-number`: build path changed from `Medication.batch.lotNumber` to `Medication.instance.lotNumber`, to match its expression.
- Release note under "Changes since 6.0.0-ballot5" (Medication).

## FHIR-57429
- `Medication.identifier` comment: the business identifier of the Medication record (text from the resolution).
- `Medication.instance.identifier`: new comment (identifier of the physical item, typically a serial number, following the Product pattern; not used for lot numbers).
- Two examples for the same product (amoxicillin 500 mg oral capsule): `medicationexample0324` – the kind (canonical: `url`, `version`; catalogue `identifier`; no `instance`); `medicationexample0325` – a physical item (stock-system `identifier`; `instance.identifier` serial number, `lotNumber`, `expirationDate`).
- Release note under "Changes since 6.0.0-ballot5" (Medication).

## Build
Summary Errors=1, not related to these changes: tx.fhir.org returned 502 Bad Gateway while validating `observation-example-glasgow`. Both new examples validate. Published output checked: search-parameters.json has `Medication-serial-number` = `Medication.instance.identifier` and `Medication-lot-number` = `Medication.instance.lotNumber`; both comments, the examples and the release notes are on the Medication pages.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `064ca22f9527`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.