# Issue

**Title:** Fix Konza adts not having the correct facility name

## Description

_[Release PRs:]_

Issues:

- https://linear.app/metriport/issue/ENG-1205

### Dependencies
None

### Description
Get the name from the proper place for Konza adts
Create a re-convert script for konza adts

### Testing
- Local
  - [x] Rerun conversion on a patient
  - [x] Send an adt to mllp server
- Staging
- [x] repeat local tests
- Production
  - [ ] Only reconvert a small portion before running the entire reconvert

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * ADT-to-FHIR conversion is HIE-aware: conversion now uses the HIE name to derive encounter IDs and facility/location details (including Konza special-casing).
  * Added a reprocessing tool to scan stored ADTs, filter by HIE, aggregate results, and optionally resend via webhook with dry-run support and JSON export.

* **Reliability**
  * Improved handling of missing or non-eligible ADTs during reprocessing with clearer progress logging and safer retries.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c22635cb4064`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.