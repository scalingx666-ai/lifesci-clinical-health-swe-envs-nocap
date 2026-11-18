# Issue

**Title:** Patient Administration R6 Batch 2

## Description

## Description
The following tickets are included in this PR
* FHIR-57419 Add case of fetal record to Mother and Newborn relationship
* FHIR-54097 Add a comment to the `reAdmission` coding to indicate why its a codeable concept and not just a boolean
* FHIR-55649 Change the Encounter.participant.type binding from extensible to preferred

And also address comments from Lloyds review
* FHIR-57336 element name should be daysOfWeek (plural), not dayOfWeek (singular)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a9102009c050`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.