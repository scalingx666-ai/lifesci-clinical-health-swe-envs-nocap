# Issue

**Title:** [SchedulingWorkspace] Show blocked time under the calendar filters

## Description

https://github.com/user-attachments/assets/410278a3-45fb-470d-989e-bbe8e41d8e8f

With a Service Facility or Visit Type filter on, every block of time disappeared from the calendar, including out-of-office blocks on calendars the filter left listed. Since #11070 the calendar drew only the Slots a drawn appointment holds, and a block is held by none.

Blocked time now stays on every calendar the filters leave listed.

## The rule

Under either filter, a Slot is drawn when:

- a drawn appointment holds it (its visit, or a buffer), or
- no loaded appointment holds it, which is blocked time.

So a hidden appointment's Slots are still hidden with it, and a block is not. Status can't tell the two apart: a block and an appointment's buffer are both `busy-unavailable`. `Appointment.slot` can.

A block has no site or visit type of its own, and doesn't need one. The filters already narrow the calendars listed to the actors at that site and offering that visit type, and Slots are only loaded for those calendars. A block on a calendar the filters remove is still hidden with its calendar.

With no filter on, nothing changes.

## Not changed

- A provider at two sites still has their visits at the other site hidden, so their calendar can look free at a time they are booked elsewhere. Blocking over such a visit gives no warning: #11317.
- The detail pane's notices keep their wording. "The calendar filters hide this blocked time." is now only reachable for a Slot an appointment holds, such as a buffer left open in the pane when a filter hides its visit.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4d8621581b26`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.