# Issue

**Title:** feat: display patient age on Patient Progress page

## Description

Description:-
Patient History shows a patient’s age when their date of birth is set, but Patient Progress did not. Age is useful context when reviewing a patient’s therapy and assessment progress, so this change adds it to the Patient Progress sidebar.

In patient_progress.js, the page calculates age from the patient’s DOB using the same years, months, and days format as Patient History, then passes it to the sidebar. In patient_progress_sidebar.html, age appears with the other patient details when a valid DOB is available. Missing, invalid, or future DOBs leave the age hidden.

Before Change:-
<img width="343" height="369" alt="image" src="https://github.com/user-attachments/assets/39e9c6d6-6a4a-4fb2-853f-45e7ba68c14e" />


After Change:-
<img width="338" height="396" alt="image" src="https://github.com/user-attachments/assets/21f7e900-77b7-424a-88c7-93a88cd1d22f" />


Changes by file:-
- patient_progress.js: Passes the calculated age to the sidebar template. The calculation uses the patient’s DOB and today’s date to derive years, months, and days.
- patient_progress_sidebar.html: Displays the age alongside the other patient details when a calculated age is available.


no-docs

Note:- needs backport to version-16-hotfix.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bd04efbe67b9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.