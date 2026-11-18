# Issue

**Title:** FHIR-54535: Clarify DocumentReference _content search behavior

## Description

## Scope
Clarify DocumentReference `_content` search behavior according to the approved resolution for [FHIR-54535](https://jira.hl7.org/browse/FHIR-54535).

## Per-Ticket Change Summary
- [FHIR-54535](https://jira.hl7.org/browse/FHIR-54535): Make searching decoded attachment data optional using MAY and remove the requirement to search attachment URLs.

## Notes on Overlaps
- No overlapping ticket implementations; this PR addresses one ticket.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5a1b865a6006`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.