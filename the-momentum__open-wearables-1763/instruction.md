# Issue

**Title:** fix: don't show invitations as sent when email delivery is not configured

## Description

## What does this change?

When neither SMTP nor Resend is configured, the Team settings said "Invitation sent successfully" and marked the invitation as sent, although nothing was sent. Now the invite dialog warns that email delivery is off and links to the [Team settings docs](https://docs.openwearables.io/developer-portal/settings/team#email-delivery), the invitation stays pending, and the dialog shows the invite link right away instead of relying on the copy button in the pending list. "Resend" becomes "Regenerate invite link". With email configured, nothing changes.

The frontend learns about it from a new `email_enabled` flag in `GET /api/v1/config`.

Stacked on #1762.

## Why?

Since #1762 makes email delivery optional in practice (SMTP or Resend, or neither), an instance without email should get a clear invite flow, not a success message for an email that never went out.

## How did you test this?

Ran the backend from this branch in Docker with the frontend dev server.

Email not configured (`GET /api/v1/config` -> `"email_enabled": false`):

<img width="1160" height="928" alt="1-invite-dialog-no-email" src="https://github.com/user-attachments/assets/62822a31-40d8-465f-91b3-2cbde9aa6a56" />

<img width="1910" height="1166" alt="2-invitation-created-link" src="https://github.com/user-attachments/assets/b5220b56-0853-4301-b5fa-d8f9ec3377ac" />


The invitation stays PENDING in the list.

SMTP to a local Mailpit (`"email_enabled": true`): the dialog looks the same as before, the invitation goes to SENT and the email arrives in Mailpit with the accept link in both the HTML and plain-text parts.

<img width="2000" height="1448" alt="3-list-sent-with-smtp" src="https://github.com/user-attachments/assets/82549264-7bb8-4d69-bd03-212657eb61e1" />

## AI usage

Claude Code (Claude Opus) for the implementation and tests; reviewed and edited by me.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

## Summary by CodeRabbit

* **New Features**
  * The app now reports whether email delivery is available.
  * When email delivery is unavailable, team invitations can still be created and shared using an invite link. The invitation dialog stays open to show the link, with messaging and actions that reflect email availability.
  * Invitation confirmations distinguish between emails sent and invite links generated.
* **Bug Fixes**
  * Email delivery warnings now include the specific configuration issue.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b8bb8ac1f476`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.