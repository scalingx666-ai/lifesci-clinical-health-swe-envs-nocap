# Issue

**Title:** add skipping ai brief

## Description

Part of ENG-1208

_[Release PRs:]_

Issues:

- https://linear.app/metriport/issue/ENG-1208

### Dependencies
- Upstream: 
- Downstream: 

### Description
Add an optional parameter that skips AI brief generation.

### Testing
- Local
  - [x] Call the consolidated refresh endpoint with no aiSkip parameter (Should generate AI Summary should upload summary to s3)
  - [x] Call the consolidated refresh endpoint with aiSkip parameter set to false (Should generate AI Summary should upload summary to s3)
  - [x] Call the consolidated refresh endpoint with aiSkip parameter set to true (should NOT generate AI Summary and instead pull from s3)
  - [x] Run DQ and make sure its not broken
- Staging
  - [x] Repeat local tests


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Add an option to use a cached AI brief when refreshing or recreating consolidated patient data; the flag is respected across APIs and flows.

* **Performance & Reliability**
  * Centralized timeout handling, improved diagnostics/logging, and safer fallback when AI briefs are missing or invalid.

* **Infrastructure**
  * New secure storage for AI briefs in non‑sandbox environments and configuration support for its bucket name.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2dfc7c26c13a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.