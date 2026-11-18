# Issue

**Title:** feat(observation): add inpatient details to Observation (backport #1307)

## Description

Issue description
Observation forms do not show which inpatient admission a patient is associated with or the patient’s inpatient status. Service Requests already show both values.

For example, when a patient is admitted and staff record a vital sign or some tests, the person reviewing the Observation should be able to see the inpatient context on that form without opening the Patient record. Add read only inpatient_record and inpatient_status fields that fetch from Patient, following the Service Request pattern.

After Change:
<img width="974" height="281" alt="image" src="https://github.com/user-attachments/assets/ce52b829-1af8-4662-9e76-13d95507dda5" />

Changes made:-
Added read only inpatient_record and inpatient_status fields to Observation. Both fetch their values from Patient, following the Service Request pattern.

Existing records
New Observations will fetch the values. Existing Observations will gain the fields, but this change does not backfill stored values. An existing draft may fetch the patient’s current values when saved; submitted Observations generally will not.

no-docs<hr>This is an automatic backport of pull request #1307 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `83e1f2cfa801`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.