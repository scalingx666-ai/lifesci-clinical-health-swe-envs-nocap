# Issue

**Title:** ENG-992 Update sanitization logic placement

## Description

Part of ENG-992

### Description

- XML Sanitization will now happen before remove b64 flow is triggered
- We only rebuild XML>JSON>XML in case b64 attachments were extracted

### Testing

- Local
  - [x] Rerun some problematic files
  - [x] Run FHIR test suite
- Production
  - [ ] Rerun DLQ
  - [ ] Check if doctor notes issues were fixed

### Release Plan
- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

- New Features
  - Automatic sanitization of CDA XML before processing to improve conversion success.
  - Concurrent retrieval of file metadata and contents for faster processing start.

- Bug Fixes
  - Prevents failures on malformed XML processing instructions.
  - Handles files without base64 attachments without altering content.
  - Clearer validation errors with more descriptive messaging (including file details).

- Refactor
  - Unified convertibility and sanitization flow across services; legacy convertibility module removed.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5612843f7019`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.