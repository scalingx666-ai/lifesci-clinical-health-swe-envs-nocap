# Issue

**Title:** OO Tickets 06/19

## Description

## HL7 FHIR Pull Request

_Note: No pull requests will be accepted against `./source` unless logged in the_ [HL7 Jira issue tracker](https://jira.hl7.org/projects/FHIR/issues/).

If you made changes to any files within `./source` please indicate the Jira tracker number this pull request is associated with: `   `

## Description

Tickets:
https://jira.hl7.org/browse/FHIR-54892
https://jira.hl7.org/browse/FHIR-54840
https://jira.hl7.org/browse/FHIR-54837
https://jira.hl7.org/browse/FHIR-54598
https://jira.hl7.org/browse/FHIR-54488

Also adding FHIR-53723 to release notes for Device, DeviceDefinition, Specimen, and SpecimenDefinition as it was missing

Separating out specimen-container-type for SpecimenDefinition because the value set and canonical url are in two places and disposition for FHIR-54488 is scoped just to Specimen.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a7e3732ab68e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.