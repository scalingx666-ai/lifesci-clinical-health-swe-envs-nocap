# Issue

**Title:** RELEASE [step_2] tcm Viewer changes - api sort & multi select

## Description

Issues:

- https://linear.app/metriport/issue/ENG-1249

### Dependencies

- none 

### Description

- 

### Testing


Check each PR.

### Release Plan

- :warning: Points to `master`
- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Filter TCM Encounters by multiple encounter classes using comma-separated or array query parameters.
  * Sort encounters by patientFirstName (ASC/DESC) and patientLastName, in addition to existing fields.
  * Cursor-based pagination now works seamlessly with name-based sorting.
  * API responses include patientFirstName and patientLastName fields in encounter items.
  * Next-page links preserve multi-value query parameters for consistent pagination across filtered/sorted views.

* **Tests**
  * Expanded test coverage for multi-class filtering, name-based sorting, and pagination behavior.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `45dfeb74254f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.