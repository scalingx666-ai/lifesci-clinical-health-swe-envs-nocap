# Issue

**Title:** PA PractitionerRole and OrganizationAffiliation Adaptions

## Description

## HL7 FHIR Pull Request

_Note: No pull requests will be accepted against `./source` unless logged in the_ [HL7 Jira issue tracker](https://jira.hl7.org/projects/FHIR/issues/).

If you made changes to any files within `./source` please indicate the Jira tracker number this pull request is associated with: `   `

## Description
Applied the following JIRA trackers to PractitionerRole:
- [FHIR-54605](https://jira.hl7.org/browse/FHIR-54605) PractitionerRole date search parameter definition clarification
- [FHIR-54568](https://jira.hl7.org/browse/FHIR-54568) PractitionerRole.contact clarification
- [FHIR-54462](https://jira.hl7.org/browse/FHIR-54462) PractitionerRole.active is a modifier

and the following ticket to PractitionerRole and OrganizationAffiliation:
- [FHIR-53853](https://jira.hl7.org/browse/FHIR-53853) PractitionerRole & OrganizationAffiliation network element was removed

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `837cd5522128`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.