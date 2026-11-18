# Issue

**Title:** ENG-1218 Filter out bad addresses from CW links

## Description

Part of ENG-1218

### Description

 - Improve the patient address schemas on Commonwell-SDK to filter out bad addresses, instead of failing the entire getExistingLinks / getProbableLinks function
 - Improve the schema not only for the `state`, but also for `line` and `city`

### Testing

- Local
  - [x] Locally test on a patient that was erroring on the request
    - [x] Make sure that now it filters for valid addresses
- Staging
  - [x] Run PD on a normal patient with good addresses
- Production
  - [ ] Rerun affected patients

### Release Plan

- [x] Release NPM packages
- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Safer address validation: trimmed fields, normalized state handling, minimum-content rules, and safe address array filtering.
  * Patient lists now automatically exclude entries missing a valid address.

* **Bug Fixes**
  * Prevents malformed/whitespace-only address lines, cities, and states from being accepted.
  * Reduces errors from inconsistent state formatting and empty inputs.

* **Refactor**
  * Demographics switched to unified safe address validation.

* **Tests**
  * Added comprehensive tests for safe address validation and filtering.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a7f5250e679b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.