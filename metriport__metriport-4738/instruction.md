# Issue

**Title:** ENG-1164 CW patient management updates

## Description

Part of ENG-1164

### Description

- Do NOT break the flow if Get Probable Links fails
- Attempt to get links multiple times if any errors are encountered
- Add a small sleep step between existing and probable links

### Testing

- Local
  - [x] Create a patient
  - [x] Link a patient
- Staging
  - [x] Link a patient
- Production
  - [ ] Rerun a few patients with errors to test it out
  - [ ] Monitor pat
  - [ ] ient management performance

### Release Plan
- [ ] Merge this
- [ ] Action:
  - [ ] Run bulk update on patients affected in the last 2 weeks

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Refactor**
  * Patient linking logic extracted into a dedicated, retry-capable module, simplifying registration, update and removal flows.

* **Bug Fixes**
  * Improved retry handling, error capture, and logging around patient link processing to increase reliability and reduce intermittent failures.

* **Chores**
  * Reduced in-file complexity by delegating linking responsibilities to the new module, streamlining maintainability and observability.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `80be8cf01fef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.