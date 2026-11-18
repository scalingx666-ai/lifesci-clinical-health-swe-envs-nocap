# Issue

**Title:** fix(ipme):- missing admitted-inpatient patient filters in Inpatient Medication Entry

## Description

Issue Description:-
Inpatient Medication Order (IPMO) filters the Patient field to only show patients with a non-empty Inpatient Record and Inpatient Status = Admitted. Inpatient Medication Entry (IPME) did not apply the same restriction, either on the main form Patient field or on the Patient field inside the medication orders table. Because of that mismatch, IPME allowed selecting patients outside the intended admitted inpatient scope.

Fix Applied
Added the same patient query filter used in IPMO to IPME also.

The fix applies to:

- IPME form-level patient field
- IPME child table patient field in medication_orders

Applied filters:
inpatient_record != ""
inpatient_status = "Admitted"

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f6dbec66f60c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.