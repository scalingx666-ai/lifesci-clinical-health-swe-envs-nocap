# Issue

**Title:** RELEASE Utils script for converter DLQ + Heartbeat monitors

## Description

Issues:

- https://linear.app/metriport/issue/ENG-000

### Dependencies

Upstream: 

### Description

- 
- 
- 
- 

### Testing

Check each PR.

### Metrics

Check each PR.

### Release Plan

- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * CSV input option for reconversion workflows; patient CSV import supported.
  * Heartbeat monitoring integration for HL7 notification service.

* **Improvements**
  * Improved CLI for message inspection with max-message and download-files options; outputs patient_ids.csv and aggregated message summary.
  * Added confirmation prompt before bulk dispatches, retry-backed dispatches, and elapsed-time logging.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `761afa923437`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.