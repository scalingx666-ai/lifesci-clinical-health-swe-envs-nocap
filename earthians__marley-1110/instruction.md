# Issue

**Title:** fix(inpatient-medication-order): skip duplicate inpatient medication order check when patient encounter is blank (backport #1100)

## Description

Issue Description:-
When creating an Inpatient Medication Order for an admitted patient without linking a Patient Encounter, the first order is saved successfully. However, any subsequent inpatient medication order without a linked encounter fails with a DuplicateEntryError.

Error shown:
                      An Inpatient Medication Order HLC-IMO-2026-00001 against Patient Encounter None already exists.

Root cause:
The duplicate validation checks only patient_encounter. When the field is empty, all records with patient_encounter = None are treated as duplicates of each other.

Fix Applied:-
Updated duplicate validation in Inpatient Medication Order to skip the duplicate check when patient_encounter is not set.

This ensures:
orders linked to a Patient Encounter still preserve the existing duplicate protection
orders created without a linked encounter are no longer incorrectly blocked as duplicates

<hr>This is an automatic backport of pull request #1100 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6a2b9741f9e2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.