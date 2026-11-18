# Issue

**Title:** fix: retain inpatient record on diagnostic reports after patient discharge (backport #1093)

## Description

When a Diagnostic Report is created for an admitted patient, the inpatient_record is fetched from the Patient master. If payment is completed and the patient is discharged before the report is saved or finalized, the Patient document no longer holds that active inpatient_record. As a result, the field can become blank on the Diagnostic Report, which breaks traceability back to the admission tied to the report.

Fix applied:-
Added fetch_if_empty: 1 to the inpatient_record field on the Diagnostic Report doctype. This keeps the already-fetched value on the report and prevents it from being overwritten with an empty value when patient.inpatient_record is cleared after discharge.<hr>This is an automatic backport of pull request #1093 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c13aaef95c83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.