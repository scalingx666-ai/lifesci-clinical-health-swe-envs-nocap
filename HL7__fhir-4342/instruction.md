# Issue

**Title:** Imaging Selection Technical corrections

## Description

## HL7 FHIR Pull Request

_Note: No pull requests will be accepted against `./source` unless logged in the_ [HL7 Jira issue tracker](https://jira.hl7.org/projects/FHIR/issues/).

If you made changes to any files within `./source` please indicate the Jira tracker number this pull request is associated with: `   `

## Description
  * FHIR-57948
    * Replace (x,y) triplets with (x,y) pairs
  * FHIR-58184
    * Remove '...' from bulleted list
  * FHIR-58180
    * Link incorrectly points to `imagingstudy.html` instead of `imagingselection.html`
  * FHIR-58183
    * Add "DICOM" before "Study" and "Series" to be consistent in usage

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1a8e2f681709`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.