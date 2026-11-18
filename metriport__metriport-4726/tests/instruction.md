# Issue

**Title:** feat(ehr): athena writebaack extra scope

## Description

Ref: ENG-1140

### Description

- adding allergies and procedures to athena auto-writeback

### Testing

- Local
  - [x] write back procedure works
  - [x] write back allergy works
- Staging
  - [x] write back procedure works
  - [x] write back allergy works
- Sandbox
  - [ ] N/A
- Production
  - [ ] write back procedure works
  - [ ] write back allergy works

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Added write-back support for Allergy and Procedure resources.
  * Enabled write-back of allergies and surgical history to Athenahealth.
  * Expanded bundle write-back to recognize and process AllergyIntolerance and Procedure resources.
  * Added per-resource write-back filters for allergy and procedure (including disable flags).
  * Broadened resource selection to include DiagnosticReports without results when other conditions permit.
  * Improved validation and routing to ensure requests reach the correct EHR implementation.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `040bd5974e4b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.