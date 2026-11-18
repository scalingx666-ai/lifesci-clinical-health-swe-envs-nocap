# Issue

**Title:** Move post-ballot entries to current release notes

## Description

## HL7 FHIR Pull Request

_Note: No pull requests will be accepted against `./source` unless logged in the_ [HL7 Jira issue tracker](https://jira.hl7.org/projects/FHIR/issues/).

If you made changes to any files within `./source` please indicate the Jira tracker number this pull request is associated with: `FHIR-58530, FHIR-58416, FHIR-58415, FHIR-58295, FHIR-58294, FHIR-58293, FHIR-58291, FHIR-58290, FHIR-58287, FHIR-57931, FHIR-57930, FHIR-24662`

## Description

Moves the 12 JIRA entries added by #4291 out of the historical **Note to Balloters for Ballot5** and into separate **Changes since 6.0.0-ballot5** sections on the Specimen, BodyStructure, ServiceRequest, and Observation resource pages. This is a release-note placement correction only; it does not change the resource definitions or examples implemented by #4291 and the related earlier PRs.

The generated pages contain each ticket link exactly once under the new heading and none in the historical Ballot5 notes. The full publisher result matches the prior baseline: 1 error, 3,754 warnings, 374 informational messages, and 0 broken links. The sole error remains the pre-existing SNOMED CT validation failure in `riskassessment-example-prognosis`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1f5adf74ce27`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.