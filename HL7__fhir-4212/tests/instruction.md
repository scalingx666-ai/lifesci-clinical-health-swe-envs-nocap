# Issue

**Title:** Ygaudet csvs 2 tho

## Description

## HL7 FHIR Pull Request

_Note: No pull requests will be accepted against `./source` unless logged in the_ [HL7 Jira issue tracker](https://jira.hl7.org/projects/FHIR/issues/).

If you made changes to any files within `./source` please indicate the Jira tracker number this pull request is associated with: `FHIR-55276, FHIR-55481, FHIR-55269,  FHIR-55264`

## Description

-We will move the DocumentRelationshipType ValueSet and CodeSystem to THO. 
-observation-interpretation-context:  change to experimental for CodeSystem and ValueSet
-observation-referencerange-normalvalue:  keep ValueSet and move CodeSystem to THO
-update the specimen-role valueset to be based on the THO code system (https://terminology.hl7.org/CodeSystem-v2-0369.html) and register the specimen-role valueset in THO
-remove the valuesets and codesystems defined in the FHIR specification as they are not used after the move the THO.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5b0e5db918d7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.