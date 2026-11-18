# Issue

**Title:** feat(ehr): fixes

## Description

Ref: ENG-1140

### Description

- make allergy manifestation optional for athena writeback
- turn on automated writeback for athena

### Testing

- Local
  - [x] write back allergies with no manifestation
- Staging
  - [x] write back allergies with no manifestation
  - [x] write back starts automatically
- Sandbox
  - [ ] N/A
- Production
  - [ ] write back allergies with no manifestation
  - [ ] write back starts automatically

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Re-enabled automated write-back for supported EHRs with upfront validation and an explicit list of allowed sources.
  * Write-back job scheduling restored when eligibility and secondary mappings validate.

* **Bug Fixes**
  * Medication and allergy lookups accept text fallbacks when standard coding is missing; display prefers coding but falls back to text.
  * Allergy reactions are only added when matched, deduplicated, and omitted when none exist; error messages simplified for missing data.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f90eac3060c6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.