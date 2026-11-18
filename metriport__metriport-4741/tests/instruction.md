# Issue

**Title:** Add ability to impersonate HIES

## Description

Part of ENG-1161

_[Release PRs:]_

Issues:

- https://linear.app/metriport/issue/ENG-1161

### Dependencies
None

### Description
Add a check for a custom segment
If segment is present "impersonate" that hie and timezone

### Testing
- Local
  - [x] send a message as Bamboo with a timezone (should NOT check for ZFA segment)
  - [x] send a message as Bamboo without a timezone (should check for ZFA segment)
  - [x] send a message as Konza without timezone (should check for PV1.39)
  - [x] send a message as Konza with timezone (should NOT check for PV1.39)
  - [x] send a message as a non-existing HIE with a timezone (should keep going using that timezone)
  - [x] send a message as a non-existing HIE with no timezone (should fail)
  - [x] send a message without the ZIT segment
- Staging
  - [x] Repeat local tests


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Extract HIE and optional impersonation timezone from an HL7 custom segment; forward impersonation timezone to webhooks and acknowledgements and accept it as an optional sender parameter.

* **Refactor**
  * Consolidated HIE/timezone resolution with improved diagnostics and logging; sender logic now prefers provided impersonation timezone.

* **Documentation**
  * Updated example/test messages to show impersonation hints; local test client host set to 127.0.0.1.

* **Tests**
  * Updated tests to use the new preprocessing helper for HIE config inputs.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bee1e5773bb4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.