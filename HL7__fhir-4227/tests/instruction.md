# Issue

**Title:** Ygaudet Observation adjustments

## Description

## HL7 FHIR Pull Request

_Note: No pull requests will be accepted against `./source` unless logged in the_ [HL7 Jira issue tracker](https://jira.hl7.org/projects/FHIR/issues/).

If you made changes to any files within `./source` please indicate the Jira tracker number this pull request is associated with: `FHIR-57418, FHIR-57447`

## Description

FHIR-57418 Renamed Observation.interpretationContext to Observation.context
FHIR-57447 Added a section in notes to raise awareness of the resource-PertainsToGoal extension

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `24057fe33448`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.