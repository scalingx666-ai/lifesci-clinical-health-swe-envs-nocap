# Issue

**Title:** ENG-1304:  add a bunch of new metadata to docrefs

## Description

### Dependencies

None

### Description

Adds a bunch of new metadata to docrefs for data coming from carequality:
High value!
- type
- category (e.g. Summarization of episode note)
- period (of service delivered)

more value!
- practiceSetting (e.g. internal medicine)
- healthcareFacilityTypeCoding (e.g. Private physicians' group office)
- document format (e.g. hl7 ccd)
- confidentiality coding

### Testing

- Local
  - [x] Run `process-dq.test.ts` to verify the extraction of the values from the ccd works correctly
  - [x] Pass old payload to /document-query/results to ensure that docref result poller works even if all new fields are missing
  - [x] Pass new payload to /document-query/results with all new fields to docref result poller and ensure that the docref appears in fhir server
- Staging
  - [x] Pass old payload to /document-query/results to ensure that docref result poller works even if all new fields are missing
  - [x] Pass new payload to /document-query/results with all new fields to docref result poller and ensure that the docref appears in fhir server
- Production
  - [ ] Trigger DQ for a patient and see if the new docref metadata appears in the patient's bundle

### Release Plan

- [ ] Release NPM packages
- [ ] FHIR Integration Test ran with validation
- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Document references now include service start/stop times, author info, creation date handling, contained organization refs, and richer coding metadata (type, class, format, confidentiality, practice setting, facility type, period/context).
  * Format fields now accept structured Coding in addition to strings; public Coding type and a Coding type-guard added; data schemas extended for new coding and temporal fields.

* **Tests**
  * Test fixtures and sample XML expanded to cover the new time and coding fields.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9a8756798a80`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.