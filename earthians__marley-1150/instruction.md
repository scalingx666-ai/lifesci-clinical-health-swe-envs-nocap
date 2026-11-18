# Issue

**Title:** fix(inpatient): inpatient discharge flow so service unit becomes vacant only on final discharge not on discharge scheduled (backport #1146)

## Description

Issue description:-
In the inpatient flow, the Healthcare Service Unit occupancy is being marked as Vacant during Order Discharge:
     Inpatient Record -> Schedule Discharge -> Order Discharge

At that point, the Inpatient Record status is still Discharge Scheduled, so the patient is not yet fully discharged. This causes the bed/service unit to appear available too early, which can lead to incorrect occupancy visibility and possible reassignment before the final discharge is completed.

Expected behavior:
The Healthcare Service Unit should remain Occupied while the Inpatient Record is Discharge Scheduled and should only be set to Vacant when the patient is finally discharged and the record moves to Discharged.

Fix / changes applied:-

- Removed the occupancy checkout call from schedule_discharge().
- Kept the Healthcare Service Unit in Occupied state during Discharge Scheduled.
- Moved the occupancy checkout logic to discharge_patient().
- Ensured the service unit is marked Vacant only when final discharge is completed.
- Updated regression tests to verify:
1. Order Discharge keeps the unit Occupied
2. final discharge changes the unit to Vacant

After-fix flow
- Patient is admitted.
- Healthcare Service Unit is set to Occupied.
- User clicks Schedule Discharge and completes Order Discharge.
- Inpatient Record status becomes Discharge Scheduled.
- Healthcare Service Unit remains Occupied.
- Final discharge is performed.
- Inpatient Record status becomes Discharged.
- Active occupancy row is checked out.
- Healthcare Service Unit is set to Vacant.

Closes issue: #1141 <hr>This is an automatic backport of pull request #1146 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `00ba48a83028`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.