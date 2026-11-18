# Issue

**Title:** Show whether a bug report was sent after submitting it

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:** 

**Description:**

After submitting the "Report a Bug" form, the user lands on the dashboard with no message, whether or not the email was sent. `processError` ignored the send result and always set a success flash, but the dashboard is now a React page that only shows flash messages passed in the URL. On a default install (mail disabled, bug reports enabled), every report is dropped silently.

`processError` now shows the success message only when the email is sent, otherwise the existing "Email was NOT sent to {0}" as an error, and passes the flash to the dashboard like `StockMovementController` does. `useFlashScopeListener` showed flash errors as an empty toast because it passed the text as `error`, so it now passes it as `message`.

---
### :camera: Screenshots & Recordings (optional)

Mail disabled or SMTP refusing the message:

<img width="696" height="243" alt="Error toast: Email was NOT sent to [errors@openboxes.com]" src="https://github.com/user-attachments/assets/434e2ed4-229d-4192-a05c-6cfcfeaa39b9" />

Mail sent:

<img width="696" height="243" alt="Success toast: Your error has been reported to [errors@openboxes.com]" src="https://github.com/user-attachments/assets/59c962ad-6821-4711-a437-22adba452e6f" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4b6ab285dc04`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.