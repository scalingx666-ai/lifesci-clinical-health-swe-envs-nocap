# Issue

**Title:** RELEASE ENG-1193 - QoL improvements + follow ons

## Description

### Dependencies

Downstream: 

### Description

- 
- 

### Testing

Check each PR.

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Summaries now include a clear sources section with explicit citation requirements and graceful handling of unknowns.
  * Expanded medical inference coverage with additional resource types (e.g., AllergyIntolerance, MedicationStatement, Procedure, Encounter, Immunization, Observation) and richer, structured questions for improved summaries.

* **Refactor**
  * Response delivery changed from streaming to a single JSON payload, returning the finalized summary text for simpler consumption and integration.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a20d018cadc3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.