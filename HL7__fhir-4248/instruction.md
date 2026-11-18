# Issue

**Title:** FHIR-43308 - Rename .prescription to .request, added RequestOrchestra…

## Description

…tion and NutritionOrder to the .request, and removed originalPrescription

Did not add .basedOn to VisionPrescription as it is already there.

Created a new ticket 57755 to hold the issues from 43308 for future consideration.

## HL7 FHIR Pull Request

_Note: No pull requests will be accepted against `./source` unless logged in the_ [HL7 Jira issue tracker](https://jira.hl7.org/projects/FHIR/issues/).

If you made changes to any files within `./source` please indicate the Jira tracker number this pull request is associated with: `   `

## Description

FHIR-43308 - Rename .prescription to .request, added RequestOrchestration and NutritionOrder to the .request, and removed originalPrescription

Did not add .basedOn to VisionPrescription as it is already there.

Created a new ticket 57755 to hold the issues from 43308 for future consideration.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7c9b62d86b08`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.