# Issue

**Title:** [SchedulingWorkspace] Configurable Appointment note max length

## Description

A host can cap Appointment.comment at a number of characters, in the booking form and when editing an appointment's details. The Notes field shows a running count, and an appointment whose notes are already over the cap can't be saved until they are shortened.

The cap is enforced only in these forms; the server accepts notes of any length.

<img width="1668" height="1206" alt="Storybook screenshot showing control and the counted Appointment Note field" src="https://github.com/user-attachments/assets/b9130730-a31e-4d59-bf5a-66c6b9c1a4f4" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d9e22944fd5b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.