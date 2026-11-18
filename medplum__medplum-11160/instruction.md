# Issue

**Title:** [SchedulingWorkspace] Shared pane header with pill tabs

## Description

The panes beside the calendar share a PaneHeader: a title, a bordered round close button, and a divider under both. The booking pane's title is replaced by its mode tabs, now pill-styled "Book Appointment" / "Block Time" tabs in the header, so the pane no longer stacks a heading above a separate tab row. The Tabs root wraps the header and the panels, so the tabs keep their tabpanel linkage.

Extracted from Kevin's `kevin-calendar-explorations` branch.

<img width="1528" height="1196" alt="Screenshot 2026-10-27 at 6 53 31 PM" src="https://github.com/user-attachments/assets/1432246f-da01-4228-b5b6-7d83585dea37" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e5b1a8ff293d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.