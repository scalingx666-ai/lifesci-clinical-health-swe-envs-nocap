# Issue

**Title:** feat(ehr): queue linking for appointment whs

## Description

Ref: ENG-1201

### Description

- switch app to queue linking for appointment WHs to decrease PG usage in realtime

### Testing

- Local
  - [ ] N/A
- Staging
  - [x] Create appointment in each EHR -- see queue process the event
- Sandbox
  - [ ] N/A
- Production
  - [ ] Queues process in realtime (vs. bulk ingest)

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

- Refactor
  - Standardized patient linking before sync in Elation and Healthie appointment webhooks.
  - Unified identifiers and handler usage for consistency across EHRs.
  - No changes to public interfaces or request/response shapes.

- Bug Fixes
  - More reliable patient matching from appointment events, reducing missed or duplicate links.
  - Improved synchronization stability and data quality during webhook processing.
  - Ensures consistent processing order: link first, then sync, for better outcomes.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `72f9913c0f3f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.