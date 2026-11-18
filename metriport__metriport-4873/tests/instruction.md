# Issue

**Title:** ENG-1275 FHIR hydration to fill in condition category

## Description

Part of ENG-1275

### Dependencies
- Downstream: 

### Description

- Added a heuristic to FHIR hydration to fill in a Condition `category`, as outlined in [this spec
](https://terminology.hl7.org/6.5.0/CodeSystem-condition-category.html)
- Added hydration for the `clinicalStatus` 
- Added unit tests

### Testing

- Local
  - [x] Unit tests
  - [x] Run on a few bundles and review results
  - [ ] Confirm validity of the bundle
- Production
  - [ ] Reprocess some patients and review their analytics on Snowflake

### Release Plan
- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Conditions are enriched with ICD‑10 when missing and use encounter + patient context for smarter categorization.

* **Improvements**
  * Clinical status handling now preserves or synthesizes standardized HL7 codings.
  * Code ranking now favors HL7/FHIR systems and known system URLs have been centralized for consistency.
  * Condition category heuristics refined to distinguish problem-list vs encounter-diagnosis.

* **Tests**
  * Expanded coverage for crosswalks, category heuristics, and clinical‑status scenarios.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9a8756798a80`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.