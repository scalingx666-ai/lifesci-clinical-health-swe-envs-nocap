# Issue

**Title:** [SchedulingWorkspace] Reveal patient info on short appointments

## Description

For appointments less than about 25 minutes in duration, the slot was too short to reveal the patient name in the second line of the `<AppointmentEvent>` content. In this scenario, we now reveal the patient name on the same line as the service type.

To make this most effective, we needed more horizontal space. We've changed the default view on `<MultiCalendar>` to be a four-day view starting from the current date. This gives each day's column about 75% more width. This feels like a good fit in general for the MultiCalendar, which we expect to have concurrent events on each day as well, which will further shrink the available space.

Some sample screenshots from a 16" MBP:

## 20 minute appointments
<img width="1840" height="1196" alt="Screenshot 2026-10-28 at 2 40 50 PM" src="https://github.com/user-attachments/assets/978f8776-c968-465c-9eaf-34b66e907336" />

## At half width due to a second overlapping event
<img width="1840" height="1196" alt="Screenshot 2026-10-28 at 2 50 48 PM" src="https://github.com/user-attachments/assets/3f097b31-5762-49be-be4e-5d3c060b9ff9" />

## 15 minute appointments
<img width="1840" height="1196" alt="Screenshot 2026-10-28 at 3 01 53 PM" src="https://github.com/user-attachments/assets/ec6dd689-1a24-47d8-b7cb-7c819622244d" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a667dfa9b4d8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.