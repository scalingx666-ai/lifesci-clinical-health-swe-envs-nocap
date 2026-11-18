# Issue

**Title:** [Scheduling] Write an appointment's notes when booking and editing it

## Description

Adds a Notes text area, saved to `Appointment.comment`, to both the booking form and the appointment edit form in AppointmentDetails. Notes are trimmed, and blank notes are left off rather than written empty. The Notes detail now shows only `comment`, so it matches what the field` edits.

The booking form asks for notes only when booking: `$reschedule` takes a time and the schedules to hold it on. It sits under the patient, so the patient and the notes are the only questions below the action that finds a time.

Since every appointment now has notes to edit, the Edit button is offered again whenever the appointment isn't locked, not only when the visit type asks for codes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5c38b433bffb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.