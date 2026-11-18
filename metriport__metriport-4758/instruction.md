# Issue

**Title:** ENG-000 Minor fix XCPD lambda

## Description

Part of ENG-000

### Description
- Grant read to lambda on the FF table

### Testing

- Staging
  - [ ] Confirm XCPD doenst alert

### Release Plan
- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Chores**
  * Updated backend permissions so the patient discovery service can read feature flags when available, enabling safer, controlled rollouts.
  * No changes to APIs, configuration inputs, or deployment workflows; existing environments require no action.
  * Backward compatible with no expected impact on performance or availability; this enhances readiness for feature-flagged behavior without altering current functionality.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fc82cd17fd07`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.