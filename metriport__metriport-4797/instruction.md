# Issue

**Title:** ENG-000 Better warning on missing consolidated when running 1-fhir-to-csv

## Description

### Dependencies

none

### Description

Better warning on missing consolidated when running `1-fhir-to-csv` for analytics ingestion

### Testing

- Local
  - [x] normal message when all pts have consolidated
  - [x] "flashy" message when missing consolidated
- Staging
  - none
- Sandbox
  - none
- Production
  - none

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added an optional check to identify patients lacking consolidated data. When enabled, the tool lists affected patient IDs and clearly logs whether all patients are covered.
  * Enhanced the confirmation prompt to include a heads-up if any patients are missing consolidated data, helping users make informed decisions before proceeding.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c2dae7a61740`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.