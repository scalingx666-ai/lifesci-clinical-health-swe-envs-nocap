# Issue

**Title:** ENG-954 bulk ingestion using original s3 prefix

## Description

### Dependencies

none

### Description

bulk ingestion using original s3 prefix

### Testing

- Local
  - [x] run bulk import and fhir-to-csv and merge generate s3 prefixes as expected (same as prod)
- Staging
  - [x] run bulk import all the way to snowflake
- Sandbox
  - none
- Production
  - [ ] run bulk import for a cx

### Release Plan

- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added a CLI flag (-l/--run-on-local) to run CSV merging locally without queueing.
  * Displays a clear “RUNNING ON LOCAL” warning when local mode is enabled.

* **Improvements**
  * Output files are now organized under patient-specific prefixes for easier navigation and management.
  * More consistent and predictable output file names and upload paths across datasets.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ba8b2768ea2d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.