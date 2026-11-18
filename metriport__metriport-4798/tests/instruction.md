# Issue

**Title:** RELEASE: ENG-530, ENG-1187

## Description

Issues:

- https://linear.app/metriport/issue/ENG-530
- https://linear.app/metriport/issue/ENG-1187

### Dependencies

- Upstream: None
- Downstream: None

### Description

- 
- 

### Testing

Check each PR.

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* New Features
  * Added a CLI command to bulk-convert Surescripts patient and batch responses to FHIR bundles, with caching, dry-run, and recreate options.
  * Persist raw XCPD requests and responses after successful sends to support traceability.
* Bug Fixes
  * For the new SOAP path, use only the first patient name and simplify address line handling to improve XCPD compatibility.
* Refactor
  * Standardized logging in Surescripts FHIR bundling and now return the hydrated bundle instead of the original.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ed3c62fc109c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.