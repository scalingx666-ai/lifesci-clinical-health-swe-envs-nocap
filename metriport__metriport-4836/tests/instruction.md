# Issue

**Title:** RELEASE feat(core) add ability to use cached ai brief on consolidated creation

## Description

_[Release PRs:]_

Issues:

- https://linear.app/metriport/issue/ENG-1208

### Dependencies

- Upstream: 
- Downstream: 

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
  - Added option to use a cached AI Brief when generating consolidated patient data, enabling faster refreshes.
  - Internal API endpoint now supports a query parameter to trigger cached AI Brief usage.

- Improvements
  - More reliable AI Brief handling with timeout safeguards and graceful fallbacks.
  - Reduced latency when a cached brief is available.

- Infrastructure
  - Introduced secure storage for AI Briefs to support caching.
  - Updated environment configuration and permissions to enable the new storage and runtime access.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ddc0733aa297`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.