# Issue

**Title:** PATCH Revert "Merge pull request #4715 from metriport/develop"

## Description

### Dependencies

None

### Description

Revert merge

### Testing

None - revert pr

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

- Refactor
  - Webhook payloads: removed requestId from metadata; messageId, when, and type remain.
  - FHIR CDA output: removed DiagnosticReport status/code; presentedForm now encodes from text.
- Documentation
  - Updated webhook and real‑time patient notification examples and schemas to omit requestId; standardized example IDs.
- Samples
  - Simplified listPatients usage to default paging.
  - Pruned .env.example by removing IS_PROD guidance/variable.
- Chores
  - Removed analytics log about patients without consolidated data.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1e9cac2a2ae5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.