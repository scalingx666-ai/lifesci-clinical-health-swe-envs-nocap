# Issue

**Title:** ENG-1193: release follow ups

## Description

### Dependencies

- Downstream: 

### Description

Rips out SSE for a synchronous call since AWS API GW does not support sse.

### Testing

Verified working locally.

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Medical inference endpoint now returns a single JSON response with the final summary, replacing streaming updates (SSE). Easier to consume and integrate with clients.
* **Documentation**
  * Updated endpoint documentation to reflect the JSON response format and example usage.
* **Chores**
  * Removed legacy streaming infrastructure and related dependencies to streamline the response flow.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a7f5250e679b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.