# Issue

**Title:** feat(api): add better prompts and cleaner citation

## Description

### Dependencies

None

### Description

Should give us better answers and makes the experience for the user less confusing w/ better citations.

### Testing

None

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

- New Features
  - Expanded support for summarizing more medical resource types, including AllergyIntolerance, MedicationStatement, Procedure, Encounter, Immunization, DiagnosticReport, and Observation.
  - Introduced a standardized “Citing claims” section with per-claim citations and a consolidated sources list using markdown links.
  - Ensured each claim is cited exactly once and duplicate sources are listed only once.
  - Updated behavior to remain silent when information is unknown, improving response precision.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9ac92e856ced`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.