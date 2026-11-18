# Issue

**Title:** feat(diagnostics): add emergency record field to sample collection and diagnostic report

## Description

When a patient is registered to ER, emergency_record is already visible in Patient Encounter and Service Request, but it was missing in Sample Collection and Diagnostic Report.

This caused ER-linked context to be inconsistent across related healthcare documents.

Expected behavior:
emergency_record should also be available in Sample Collection and Diagnostic Report, similar to how related patient-linked fields are shown there.

Fix Applied / Changes Applied:-

- Added emergency_record to Diagnostic Report field metadata.
- Added emergency_record to Sample Collection field metadata.
- Set both fields to fetch from patient.emergency_record.

Note:-
Matched existing DocType behavior:
- Diagnostic Report uses fetch_if_empty, same as its inpatient_record field.
- Sample Collection does not use fetch_if_empty, matching its current inpatient_record setup.

no-docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `380aceb6e9a8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.