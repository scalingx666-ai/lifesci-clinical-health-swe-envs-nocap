# Issue

**Title:** [SchedulingWorkspace] Position workspace controls in calendar toolbar

## Description

- Adds the ability for the Calendar components to have toolbar entries inserted at front and tail positions.
- Moves the sidebar collapse toggle into the `toolbarStart` position
- Adds a "New Appointment" button in the `toolbarEnd` position

Extracted from Kevin's kevin-calendar-explorations branch.

https://github.com/user-attachments/assets/05e44f76-0e73-492d-ab8e-03337915f69b

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aaca7d552f56`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.