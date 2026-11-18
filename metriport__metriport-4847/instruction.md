# Issue

**Title:** ENG-1237: feat(core): add cloudwatch reporting metrics to webhook sender

## Description

### Dependencies

None

### Description

Add metrics for cloudwatch reporting (so we can set up an alarm) 

Cost analysis (monthly) for current metrics: 
- LLM inference metrics:
  - 3 metrics, $0.30 / cx => $0.90 / cx 
- Roster upload metrics 
  - By customer: $0.30 / cx / hie (only happens + is billed if the pairing actually exists)
- Incoming ADT notifications
  - By customer: $0.30 / cx / hie (only happens + is billed if the pairing actually exists)
    - Priced the same as the above roster upload metric.
  - By ADT event type: ~ $5 / integrated hie. 

### Testing

- Local
  - [x] Branch to staging, ensure metric is logged and ADTs continue to run without error.
- Staging
  - [x]  Branch to staging was successful
- Production
  - [ ] ensure metric is logged and ADTs continue to run without error.

### Release Plan

- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Added advanced metric reporting for richer CloudWatch telemetry (multi-metric payloads and validation).

* **Refactor**
  * Parallelized analytics and metric reporting to reduce end-to-end latency for notifications, roster uploads, and inference flows.

* **Chores**
  * Consolidated emitted metrics and standardized dimensions for clearer per-customer, event-type, and service-level observability.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `910af28c6211`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.