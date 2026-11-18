# Issue

**Title:** [Scheduling] Hide deceased patients from the patient picker, and mark them on appointments

## Description

Deceased patients will no longer be offered in the booking form's patient picker. The exception is exact MRN matches, which are still listed, marked "Deceased" (so that users looking for exact patients can see they exist). Picking one shows an error and blocks booking. Otherwise they will not appear in the dropdown.

<img width="680" height="260" alt="image" src="https://github.com/user-attachments/assets/9e68c077-f831-44a0-a807-24da7b8ca1a2" />

<img width="459" height="128" alt="image" src="https://github.com/user-attachments/assets/43128168-f304-4a10-a2f6-5b2f9c53f195" />

Existing appointments with a deceased patient will have "(deceased)" appended to the patient's name on the calendar event, hover card, and details pane.

<img width="780" height="510" alt="image" src="https://github.com/user-attachments/assets/c8e6e1f0-f252-484b-bd1f-28b3893932f3" />

<img width="1110" height="480" alt="image" src="https://github.com/user-attachments/assets/2455675d-d422-4de0-99bc-5b850f555893" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a8d70aa5e644`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.