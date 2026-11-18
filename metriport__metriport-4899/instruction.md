# Issue

**Title:** ENG-630 Small adj on util script

## Description

### Dependencies

- Upstream: 
- Downstream: none

### Description

- missed fixing the timeout on axios for process-dlq-xmls (just a script)

### Testing

- Local
  - none
- Staging
  - none
- Sandbox
  - none
- Production
  - none

### Metrics

none

### Release Plan

- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Bug Fixes**
  * Corrected HTTP timeout handling so stalled requests time out as intended (now 30s), improving reliability of remote calls.
* **Chores**
  * Tuned DLQ processing: limited parallel conversions and added jitter between retries to reduce spikes and improve stability.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `79b093bc1ede`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.