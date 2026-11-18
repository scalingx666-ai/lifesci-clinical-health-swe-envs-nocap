# Issue

**Title:** [SchedulingWorkspace] Move day selection widget into time finder pane

## Description

Extracts changes to Time Finding in the `<SchedulingWorkspace>` component from `kevin-calendar-explorations`.

- Moves the day selection widget from the main Appointment booking form into the time finder pane
- Adds a header to that pane
- Adjusts styles on CalendarDateInput to make the month switcher buttons more subtle and aligned to the month grid

https://github.com/user-attachments/assets/9ea1c39c-bf7b-4520-99a4-3bf6d08bef67

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `81d38472958a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.