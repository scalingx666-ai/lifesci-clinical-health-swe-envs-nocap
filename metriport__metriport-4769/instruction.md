# Issue

**Title:** add raw incoming bucket to mllp server

## Description

Part of ENG-1162

_[Release PRs:]_

Issues:

- https://linear.app/metriport/issue/ENG-1162

### Dependencies

- Upstream: 

### Description
Adds a raw incoming bucket to mllp server so we never lose any adts.

### Testing
- Local
  - [x] Test on local

<img width="658" height="511" alt="Screenshot 2025-09-29 at 2 41 37 PM" src="https://github.com/user-attachments/assets/7a643c62-8cdf-424d-9b45-7ce3e7cc60f2" />

- Staging
  - [x] Test on staging


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

- New Features
  - Raw incoming HL7 messages are uploaded to S3 before processing; upload failures are logged but do not block handling.
- Infrastructure
  - A private, encrypted, versioned S3 bucket is provisioned for raw HL7 messages with CORS allowing uploads.
- Configuration
  - Added a required configuration setting for the raw HL7 message bucket; example config updated.
- Refactor
  - Internal references updated to use the new raw HL7 bucket across stacks and services.
- Tests
  - Tests adjusted to reference the new configuration path.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f72a532f3a88`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.