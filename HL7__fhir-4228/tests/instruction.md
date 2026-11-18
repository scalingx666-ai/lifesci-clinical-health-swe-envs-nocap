# Issue

**Title:** FHIR-57238 Added constraint to Claim.insurance and ExplanationOfBenef…

## Description

…it.insurance to ensure one entry has focal=true.

## HL7 FHIR Pull Request

_Note: No pull requests will be accepted against `./source` unless logged in the_ [HL7 Jira issue tracker](https://jira.hl7.org/projects/FHIR/issues/).

If you made changes to any files within `./source` please indicate the Jira tracker number this pull request is associated with: `   `

## Description

FHIR-57238 Added constraint to Claim.insurance and ExplanationOfBenefit.insurance to ensure one entry has focal=true.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8adc6c78b3b6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.