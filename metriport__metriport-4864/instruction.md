# Issue

**Title:** ENG-1249: [step_2] tcm Viewer changes - api sort & multi select

## Description

Issues:

- https://linear.app/metriport/issue/ENG-1249

### Dependencies

- Upstream: 

### Description

Filter by multi class & allow firstName and lastName sorting in tcm viewer. 

### Testing

- Local
  - [x] backward compatible
  - [x] sorting work by firstname and lastname
  - [x] allow multi class filter
- Staging
  - [x] backward compatible
- Sandbox
  - none
- Production
  - none


### Release Plan

- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Filter TCM encounters by multiple classes in one request (accepts array or CSV; inputs normalize to arrays).
  * Encounter list items now include patientFirstName and patientLastName; sorting supports these name fields (including JSONB-backed paths) with ASC/DESC.
  * Pagination preserves multi-value query params in next-page links; cursor-based pagination and ordering improved for name-based sorts.

* **Tests**
  * Added tests for multi-class filtering, patient-name sorting (asc/desc), and cursor pagination with name-based sort fields.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `149c662b4152`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.