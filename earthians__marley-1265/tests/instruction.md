# Issue

**Title:** feat: show patient age in Patient History sidebar

## Description

PR description:

Patient age is important context when reviewing medical history and interpreting clinical records. This change displays the patient’s current age directly in the Patient History sidebar, below Contact, so clinicians/doctors can see it while reviewing the record.

Age is calculated from the DOB entered on the Patient form and shown in years, months, and days (for example, 2Y 3M 5D). If no DOB is recorded, the Age row is hidden rather than showing an unknown or misleading value.

Changes done:

- Passed the calculated age to the sidebar template.
- Added a conditional Age row below Contact.

Before:-
<img width="525" height="587" alt="image" src="https://github.com/user-attachments/assets/587fc387-fa62-4297-9e8a-ace161818e7b" />

<img width="373" height="304" alt="image" src="https://github.com/user-attachments/assets/63195c25-f032-4cda-8cdf-0a7bc605b680" />


After:-
<img width="554" height="574" alt="image" src="https://github.com/user-attachments/assets/779af5b8-2289-46c9-a345-63c892ae2981" />

<img width="368" height="283" alt="image" src="https://github.com/user-attachments/assets/a2d8d6c1-ac0c-4221-a8f6-6052072720ee" />



no-docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c9c6138ad439`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.