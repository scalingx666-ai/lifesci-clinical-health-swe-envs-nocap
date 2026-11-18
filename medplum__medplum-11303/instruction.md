# Issue

**Title:** [Scheduling] Add weekday view

## Description

- The view picker changed from a SegmentedControl to a dropdown (including in Provider app)
- All view types are available in all calendars (including in Provider app)
- Added a new "Weekdays" view that shows M-F only
- SchedulingWorkspace defaults to "Weekdays" view during weekdays. (Defaults to "Week" view on weekends).
- Creating an appointment or time block on a weekend when the view is "Weekdays" changes to the "Week" view to reveal the newly created entry.

https://github.com/user-attachments/assets/1445d815-cfab-4989-8699-e5cb40501981

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2f583b2aa78d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.