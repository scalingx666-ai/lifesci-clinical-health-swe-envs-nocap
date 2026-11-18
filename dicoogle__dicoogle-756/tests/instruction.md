# Issue

**Title:** Advertise the new UI in the current webapp

## Description

An alternative to #753. Rather than implementing a way to force users into the new webapp, provide links from the old one inviting them in.

- add a button to try the new UI in the login page
- add a link to the new webapp in the topbar

<img width="781" height="412" alt="Screenshot 2026-10-29 164711" src="https://github.com/user-attachments/assets/884afb6b-9d8b-443f-bc7a-fe8e3d751cdc" />

<img width="1341" height="391" alt="Screenshot 2026-10-29 164613" src="https://github.com/user-attachments/assets/21dc71cb-5552-4a8b-88fa-b7196f704b74" />


### Open concerns

- Is the button on the login page too big perhaps?
- Is the link in the top page clear that it's a link to the new page, and _not_ a description of the UI that the user is currently in?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1071b98f558e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.