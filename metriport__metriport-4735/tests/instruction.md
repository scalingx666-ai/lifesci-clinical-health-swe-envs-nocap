# Issue

**Title:** fix(mllp): fix remap removing parts of original data

## Description

Part of ENG-1122

_[Release PRs:]_

Issues:

- https://linear.app/metriport/issue/ENG-1122

### Dependencies
None
### Description
Remap function was deleting data, make it not delete data.

### Testing
- Local
  - [x] Run it

pid before remap: PID|1||GWIbJvTlzM5BlY11O0Y1Yt==_gX261tOzr+qgVJl2ijSgWg==^^METRIPORTPA^MR|....
pid after remap: PID|1||GWIbJvTlzM5BlY11O0Y1Yt==_gX261tOzr+qgVJl2ijSgWg==^^METRIPORTPA^MR|...

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

- New Features
  - None

- Bug Fixes
  - Corrected handling of patient identifiers during HL7v2 to FHIR conversion to prevent missing or duplicated IDs.
  - Added safeguards and clearer errors for malformed messages, reducing unexpected failures.

- Refactor
  - Streamlined patient ID update logic for greater stability and consistency.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e3f73fa1cfa2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.