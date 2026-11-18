# Issue

**Title:** Fix #1079 multiple administrations.

## Description

There was a bug that multiple medication administrations were not being output on a patient record unless that medication was also ended for each administration.

However, ending the medication after every administration is not a good idea, because that patient could also have an open prescription for that medication.

This fix ensures that MedicationAdministrations and open ongoing prescriptions of the same medications do not conflict, and both are recorded in the output files.

You can replicate the error on `master` and the fix on this branch using the below modules (looking for an annual inpatient encounters called "Dummy Encounter" and Medication/MedicationAdministration named "Administered Injection", "Chronic Injection", and "Administered Chronic Injection").

[medication_administration_example.json.zip](https://github.com/synthetichealth/synthea/files/8805896/medication_administration_example.json.zip)
[medication_administration_example_2.json.zip](https://github.com/synthetichealth/synthea/files/8809570/medication_administration_example_2.json.zip)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d90b4e3b1c41`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.