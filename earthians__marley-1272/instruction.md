# Issue

**Title:** fix: close active nursing care plans on inpatient discharge & prevent active care plans for discharged admissions (backport #1233)

## Description

Issue description:
  When an inpatient record was discharged, the linked Nursing Care Plan could remain in Active status. This caused the
  admission-specific care plan to stay open even after the patient’s inpatient stay had ended.

Changes made:

Inpatient Record changes:-
Added a helper in the inpatient discharge flow to find Nursing Care Plans linked to the discharged Inpatient Record
with status set to Active. Each matching plan is loaded, its status is changed to Closed, and it is saved. The lookup
does not use docstatus; it only checks the linked inpatient_record and active status. A regression test was added to
verify that an active Nursing Care Plan is closed when the linked Inpatient Record is discharged.

Nursing Care plan changes:-
  Added validation on Nursing Care Plan to reject active care plans linked to Discharged or Cancelled Inpatient Records.
  This prevents a race where a new care plan could be created after the discharge flow closes existing active plans.

<img width="869" height="363" alt="image" src="https://github.com/user-attachments/assets/ef75188a-4c38-44a8-84f2-721b30b3a6d4" />

  Why:
  The discharge flow only closes care plans found at that moment. Validating at the Nursing Care Plan level ensures no
  active plan can remain or be created for an admission that has already ended.

  Flow after fix:
  When the patient is discharged, the existing discharge validations run first. The system checks out the inpatient
  occupancy, sets the Inpatient Record status to Discharged, and saves it. After the Inpatient Record is successfully
  saved, the system looks for active Nursing Care Plans linked to that same Inpatient Record. If any are found, they are
  marked Closed; if none exist, nothing else happens.<hr>This is an automatic backport of pull request #1233 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `118e334ac241`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.