# Issue

**Title:** Fhir 54703 procedure bodysite bodystructure consolidation

## Description

## HL7 FHIR Pull Request

_Note: No pull requests will be accepted against `./source` unless logged in the_ [HL7 Jira issue tracker](https://jira.hl7.org/projects/FHIR/issues/).

If you made changes to any files within `./source` please indicate the Jira tracker number this pull request is associated with: `FHIR-54703`

## Description

Per FHIR-54703

Changes made to the Procedure resource:

source/procedure/structuredefinition-Procedure.xml
- Removed Procedure.bodySite element entirely
- Removed con-4 constraint (mutual exclusion between bodySite and bodyStructure)
- Updated Procedure.bodyStructure:
  - Changed type from Reference(BodyStructure) to CodeableReference(BodyStructure)
  - Changed max from 1 to *
  - Added binding to http://hl7.org/fhir/ValueSet/body-site (same as bodySite was bound to)
  - Updated short, definition, and committee-notes
  - Added mappings from bodySite

source/procedure/procedure-introduction.xml
- Added ballot note entry under Non-Compatible Changes

Note: Search parameter changes are deferred pending further OO work group discussion per May 2026 WGM.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `19d269fa4ff0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.