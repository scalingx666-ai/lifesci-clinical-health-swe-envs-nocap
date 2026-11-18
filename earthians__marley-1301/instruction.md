# Issue

**Title:** fix(patient): calculate age using calendar months and days (backport #1275)

## Description

Issue description
The Patient form calculated age from elapsed time, while Patient History used completed calendar months and remaining days, similar to age calculator. For a patient born on February 29, 2020, this could make the form differ by one day from Patient History.

Age Calculator:-
<img width="666" height="574" alt="image" src="https://github.com/user-attachments/assets/91771e58-db2e-4f38-a5e2-6fce027fed1b" />

Before:
<img width="552" height="570" alt="image" src="https://github.com/user-attachments/assets/e71c91b5-7b8e-4f67-ab74-7a1c1c930b1e" />
<img width="422" height="277" alt="image" src="https://github.com/user-attachments/assets/fe6a6e54-e2ba-4122-aba4-84bf5ca71750" />

After:-
<img width="534" height="568" alt="image" src="https://github.com/user-attachments/assets/3e128904-edef-41f5-bfc9-101141085d0e" />
<img width="351" height="264" alt="image" src="https://github.com/user-attachments/assets/a9613612-d56d-42f7-953f-3495c422bc7a" />

Fix applied
The Patient form’s get_age() function previously subtracted the DOB from the current time and passed the elapsed milliseconds to moment.duration(). That duration was then split into years, months, and days. Because calendar months have different lengths, this could produce a one-day difference for a leap-day DOB.

 changed patient.jsto use the same calendar calculation as Patient History:

1. Parse the DOB and today as strict YYYY-MM-DD dates.
2. Count the completed calendar months between them.
3. Split those months into years and remaining months.
4. Add the completed months to the DOB, then count the remaining days.

changed the form’s future-DOB validation to compare those calendar dates.

For February 29, 2020 → October 24, 2026, the form now displays 6 years, 7 months, 25 days, matching Patient History.<hr>This is an automatic backport of pull request #1275 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c46eeb49a580`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.