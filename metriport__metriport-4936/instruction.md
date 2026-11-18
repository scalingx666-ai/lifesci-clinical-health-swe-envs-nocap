# Issue

**Title:** RELEASE Avoid hitting rate limiting on checkly's heartbeat api

## Description

_[Release PRs:]_

Issues:

- https://linear.app/metriport/issue/ENG-1352

### Dependencies
None

### Description
- 

### Testing
Check each PR.

### Release Plan
- :warning: Points to `master`
- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added outbound rate limiting capability to manage request frequency to external services.
  * Enhanced heartbeat monitoring with rate limiting to prevent excessive pings to monitoring services.
  * Improved monitoring service reliability with retry logic for specific HTTP status codes (500, 502, 503, 504).

* **Infrastructure**
  * New database table provisioned to support outbound rate limiting.
  * Updated configuration to expose outbound rate limit settings across services.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a6a2f6ededda`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.