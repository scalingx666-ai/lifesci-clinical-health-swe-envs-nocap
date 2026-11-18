# Issue

**Title:** ENG-1160: Fix CW v2 DocRef creation algo

## Description

### Description
- Now CW v2 DocRefs will use a backup field for document names
- DocRef.contained is now filled in with the `Organization.name`

### Testing

- Staging
  - [x] Run DQ on a staging pt and make sure the doc details are there on the dashboard
- Production
  - [ ] Rerun for an existing patient with this problem and confirm the fix

### Release Plan
- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Documents can embed contained resources (e.g., Organization) so records are are more self-contained.
  * Document references now include a description, using the provided description or falling back to the first attachment’s title.

* **Stability**
  * Embedded resources are validated; invalid or unsupported items are skipped and logged to maintain data integrity.

* **Chores**
  * Minor import path adjustment with no runtime behavior change.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e3f73fa1cfa2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.