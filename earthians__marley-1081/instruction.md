# Issue

**Title:** fix(encounter):  Patient Encounter series when created from Patient Appointment

## Description

Issue description: 
Creating a Patient Encounter from the Create button on Patient Appointment was incorrectly carrying over the appointment’s naming_series through get_mapped_doc() in make_encounter(). Because of that, encounters created from appointments could use the wrong series and produce an incorrect sequence. Directly created Patient Encounter records did not have this problem because they used the encounter doctype’s own naming logic.

Fix applied:
 Added field_no_map: ["naming_series"] to the server-side get_mapped_doc() mapping in patient_appointment.py. This prevents naming_series from being copied from Patient Appointment to Patient Encounter, allowing the encounter to resolve its own configured series.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0c0bc59d556a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.