# Issue

**Title:** RELEASE ehr Epic documentation & improve FF test file + Posthog api key fix for webhook sender

## Description

Issues:

- https://linear.app/metriport/issue/ENG-000
- https://linear.app/metriport/issue/ENG-1100
- https://linear.app/metriport/issue/ENG-1171

### Dependencies

- none

### Description

- 
- 
- 
- 

### Testing

Check each PR.

### Release Plan

- :warning: Points to `master`
- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

- **Documentation**
  - Added an Epic EHR app page (integration overview, getting started, patient workflow, SMART on FHIR R4 scopes, OAuth 2.0 SSO).
  - Updated EHR Apps overview to include an Epic card and improved image formatting.
  - Expanded site navigation to include the Epic docs.
- **Tests**
  - Clarified test comments and adjusted example test data by disabling a sample feature flag.
- **Chores**
  - Added analytics configuration and secret usage for HL7 notification processing.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dfbbb9c67550`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.