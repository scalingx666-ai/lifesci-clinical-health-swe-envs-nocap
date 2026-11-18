# Issue

**Title:** PATCH RELEASE ENG-630 Don't retry on 500 and Fix FHIR converter error handling

## Description

### Dependencies

none

### Description

- **fix(core): don't retry on 500, ECONNRESET, ERR_BAD_RESPONSE**
- **refactor(lambda): get actual error message from the FHIR converter**
- **fix(fhir-converter): don't clog when a message fails**
- **refactor(utils): utils scripts**

### Testing

- Local
  - [x] convert failed messages from DLQ w/o clogging the converter
  - [x] convert proper messages successfully
- Staging
  - none
- Sandbox
  - none
- Production
  - [ ] reprocess DLQ

### Metrics

none

### Release Plan

- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  - Added diagnostic utilities for inspecting queue messages and converting XML payloads to FHIR format.

* **Bug Fixes**
  - Improved error handling and resource cleanup in the conversion pipeline to ensure proper state management.
  - Enhanced multi-part payload processing with consolidated bundle output.
  - Simplified retry logic for network-level errors.

* **Tests**
  - Updated connection error handling assertions to reflect behavior changes.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f03dd3f501a5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.