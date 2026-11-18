# Issue

**Title:** [SchedulingWorkspace] Appointment patients are not editable

## Description

In some downstream systems, editing a Patient is not a supported operation. Users should cancel the appointment and create a new one with the correct patient instead of editing to change this field.

Remove the patient field from the appointment edit form. The visit type's codes are now the only editable fields, so the Edit button is shown only when the visit type asks for some.

Future follow up thought: in some scenarios where the wrong patient was selected, we may want to set `Appointment.status` to "entered-in-error" instead of "cancelled". This may suggest a future enhancement to the `Appointment/$cancel` operation to take a status code, and some UI in this component to allow the viewer to set that status instead of or in addition to the cancellation reason.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `35f70cf8e436`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.