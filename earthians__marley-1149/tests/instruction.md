# Issue

**Title:** fix(inpatient): allow discharge when pending healthcare services override is enabled in healthcare settings (backport #1147)

## Description

Issue Description:-
When Healthcare Settings.allow_discharge_despite_pending_healthcare_services was enabled, inpatient discharge was still being blocked if there were submitted Service Request records linked to the inpatient record whose status was not completed.

The problem was in inpatient_record.py : the guard in validate_incomplete_service_requests(inpatient_record) was inverted. Instead of skipping validation when the override setting was enabled, it continued into the pending-service check and threw Incomplete Services.

Fix Applied:-

- In inpatient_record.py , changed the condition so the function returns immediately when         allow_discharge_despite_pending_healthcare_services is enabled.

- Added a new test in test_inpatient_record.py, named test_allow_discharge_despite_pending_healthcare_services and a small helper  to create a pending submitted Service Request linked to the inpatient record.

Flow After Fix
1. Discharge is triggered for an inpatient record.
2. discharge_patient() calls validate_inpatient_invoicing().
3. If allow_discharge_despite_unbilled_services is enabled, invoice blocking is skipped.
4. discharge_patient() then calls validate_incomplete_service_requests().
5. If allow_discharge_despite_pending_healthcare_services is enabled, the function now returns immediately.
6. No validation error is raised for pending submitted Service Request records.
7. Checkout proceeds, occupancy is marked vacant, and the inpatient record is discharged.<hr>This is an automatic backport of pull request #1147 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a2f1de321e28`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.