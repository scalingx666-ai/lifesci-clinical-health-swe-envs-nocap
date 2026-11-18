# Issue

**Title:** [ENG-747] Patient age format

## Description

## Changes

- Enhances patient age format
- ENG-747

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Improved patient age display consistently across encounters, appointments, queues, billing, and patient info views with a shared `PatientAge` component.
  * Added an optional tooltip that shows a verbose `years / months / days` breakdown when date of birth is available.
* **Enhancements**
  * Reworked age formatting to calculate elapsed time from date of birth to death/current date with tiered units (including weeks + days), supporting abbreviated output; shows “Age unknown”/“Born …” when date of birth is missing.
* **Tests**
  * Updated patient registration assertions to match the revised “Born on {year}, Male” output.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `53ae68320703`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.