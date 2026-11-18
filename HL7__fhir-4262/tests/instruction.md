# Issue

**Title:** Br cds changes 2026 06 30

## Description

* [FHIR-53716](https://jira.hl7.org/browse/FHIR-53716): Updated security category for knowledge artifacts to business
* [FHIR-53715](https://jira.hl7.org/browse/FHIR-53715): Added module and date search parameters to GuidanceResponse
* [FHIR-53714](https://jira.hl7.org/browse/FHIR-53714): Added the ability to capture input parameters in a GuidanceResponse
* [FHIR-53712](https://jira.hl7.org/browse/FHIR-53712): Added GuidanceResponse.indicator, bound extensible to CDS Hooks indicators
* [FHIR-53710](https://jira.hl7.org/browse/FHIR-53710): Added GuidanceResponse.topic and related search parameter.
* [FHIR-53413](https://jira.hl7.org/browse/FHIR-53413): Added library element to support any logic used by the event definition

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a184fb8bad39`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.