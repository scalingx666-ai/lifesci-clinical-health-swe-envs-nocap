# Issue

**Title:** RELEASE konza mapping fix + backfill script

## Description

_[Release PRs:]_

Issues:

- https://linear.app/metriport/issue/ENG-1205

### Dependencies
None

### Description
- 
- 

### Testing
Check each PR.

### Release Plan
- :warning: Points to `master`
- [ ] Run backfill script
- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

- **New Features**
  - ADT-to-FHIR processing is now HIE-aware: encounter IDs and facility/location names adapt to the originating HIE (e.g., Konza) for more accurate records and consistent downstream handling.

- **Chores**
  - Added a utility to scan S3 for ADT messages (filters Konza/HIE messages) and optionally resend them to a webhook, with dry-run support and timestamped JSON output for auditing.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1228e2f0beb4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.