# Issue

**Title:** feat(core): adding refresh on consolidated after every ADT

## Description

Part of ENG-1208

_[Release PRs:]_

Issues:

- https://linear.app/metriport/issue/ENG-1208

### Dependencies
Upstream: 

### Description
Refresh consolidated after every adt
Bring posthog analytics back to before 

### Testing
- Local
  - [x] Make sure consolidated gets new adt resources
- Staging
  - [x] Make sure consolidated gets new adt resources
  - [x] Make sure posthog still works


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Trigger conditional consolidated refreshes for specific HL7 events (A01, A03) and include a cached-AI-brief flag when applicable.
  * Move analytics reporting earlier in the notification flow with non-blocking error handling.

* **Reliability**
  * Prefer cached AI-brief retrieval when available to reduce latency.
  * Add retry-aware consolidated-refresh calls and extra logging for observability.

* **API Changes**
  * Renamed cached-AI-brief retrieval helper and updated an async call to accept a useCachedAiBrief flag.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d791d59161de`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.