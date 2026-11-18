# Issue

**Title:** fix(therapy-sessions): show Counts Completed in Therapy Session exercise child table

## Description

Issue description:
- Counts Completed was hidden in Therapy Session exercise rows.
- Root cause was a wrong depends_on condition in the shared Exercise child doctype.
- Field was checking for parenttype Therapy instead of Therapy Session.

Steps to reproduce:
- Create/use a Therapy Type with exercises.
- Create a Therapy Plan for a patient or create an encounter and select the therapy type and submit the encounter , therapy plan will be created automatically.
- Create a draft Therapy Session or create from service request if from encounter.
- Open an exercise row in the session.
- See that Counts Completed is missing.

Expected:
Counts Completed should be visible and editable in Therapy Session.

Observed:
Counts Completed was not properly shown when clicked on pencil icon.

Fix applied:
Updated depends_on in exercise.json
From: eval:doc.parenttype=="Therapy";
To: eval:doc.parenttype=="Therapy Session";

After fix:
User must be able to enter counts completed , before submitting therapy session.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `380aceb6e9a8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.