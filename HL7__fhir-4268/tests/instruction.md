# Issue

**Title:** Fhir 54987 condition bodysite bodystructure consolidation

## Description

## HL7 FHIR Pull Request
_Note: No pull requests will be accepted against `./source` unless logged in the_ [HL7 Jira issue tracker](https://jira.hl7.org/projects/FHIR/issues/).
If you made changes to any files within `./source` please indicate the Jira tracker number this pull request is associated with: `FHIR-54987`

## Description

Per FHIR-54987

Changes made to the Condition resource:

source/condition/structuredefinition-Condition.xml
- Removed Condition.bodySite element entirely
- Removed con-4 constraint (mutual exclusion between bodySite and bodyStructure)
- Updated Condition.bodyStructure:
  - Changed type from Reference(BodyStructure) to CodeableReference(BodyStructure)
  - Changed max from 1 to *
  - Added binding to http://hl7.org/fhir/ValueSet/body-site (same as bodySite was bound to)
  - Updated short, definition, and comment
  - Added mappings from bodySite

source/condition/bundle-Condition-search-params.xml
- Removed body-site search parameter
- Added body-structure-code search parameter (bodyStructure.concept)
- Added body-structure-reference search parameter (bodyStructure.reference)

source/condition/condition-introduction.xml
- Added ballot note entry under Non-Compatible Changes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a2a7cf4cde1f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.