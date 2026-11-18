# Issue

**Title:** feat(ap): configuration files

## Description

Ref: ENG-1233

Issues:

- https://linear.app/metriport/issue/ENG-1233

### Dependencies

- Downstream: transform itself

### Description

- updating configurations to remove some files and add some entires

### Testing

- Local
  - [ ] N/A
- Staging
  - [ ] re-ingest staging org
- Sandbox
  - [ ] N/A
- Production
  - [ ] re-ingest CX orgs

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Broader data extraction across clinical resources: deeper nested fields, more coding variants, and extended multi-instance support (identifiers, notes, performers, reasons, results).
  * Added granular mappings for timing, comparators, quantities, stages, and reference links to improve clinical completeness.
  * Harmonized naming for note/author fields and reorganized repeated elements for more consistent, alphabetized output; some legacy deep-index fields were removed.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3b4954e979b5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.