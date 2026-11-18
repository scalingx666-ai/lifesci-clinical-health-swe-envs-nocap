# Issue

**Title:** RELEASE refresh consolidated on every adt (but skip ai regeneration :) )

## Description

_[Release PRs:]_

Issues:

- https://linear.app/metriport/issue/ENG-1208

### Dependencies

- Upstream: 

### Description
- 

### Testing

Check each PR.

### Release Plan

- :warning: Points to `master`
- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

- New Features
  - Added option to use a cached AI Brief for faster responses, with automatic generation when missing.
  - Automatic consolidated data refresh triggered for specific HL7 events (A01, A03).

- Improvements
  - Reduced latency and improved reliability for AI Brief retrieval through cache-first logic with graceful fallback.
  - Enhanced HL7 notification handling with smarter routing and non-blocking analytics, improving observability without impacting delivery.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1950c68cf808`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.