# Issue

**Title:** ENG-1109 CCDA preprocessing fix

## Description

Part of ENG-1109

### Description

- Updated XML preprocessing before conversion to keep the order of the formatting HTML tags, making the doctors notes look as intended
- Updated resource counts

### Testing

- Local
  - [x] Test with a patient's bundle to see that the notes now look good
  - [x] Run FHIR test suite
- Staging
  - [x] Rerun a patient conversion
- Production
  - [x] Reprocess a specific patient to verify the fix
  - [ ] Reprocess all of the specific CX patients

### Release Plan
- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Bug Fixes**
  * XML parsing and generation now preserve the original element and text order, preventing unexpected reordering in outputs.
  * Whitespace in text values is retained during parsing and serialization, ensuring exact content fidelity.
  * Overall XML handling is more faithful to source documents, reducing unnecessary diffs and formatting churn in exported or processed files.
  * No functional changes to workflows; improvements focus on consistent, predictable XML formatting and content preservation.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7b188cff293d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.