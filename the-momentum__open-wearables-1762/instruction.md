# Issue

**Title:** feat(backend): support SMTP for invitation emails

## Description

## What does this change?

Until now, sending invitation emails required a Resend account, so everyone self-hosting Open Wearables had to sign up for one more third-party service, even if they already had a mail provider. This PR adds SMTP as an alternative: if `SMTP_HOST` is set we use it, otherwise Resend as before. Config is described in the [Team settings docs](https://docs.openwearables.io/developer-portal/settings/team#email-delivery).

## Why?

Almost every mail provider offers SMTP (Google Workspace, Microsoft 365, SES, Azure Communication Services, company relays), so one generic transport lets instance owners use what they already have, without provider-specific code.

SMTP is written on the stdlib, with no new dependency. I kept the Resend path instead of switching everything to Resend's SMTP endpoint for two reasons: instances that already use the Resend API keep working without any config change, and some hosting platforms block outbound SMTP ports (e.g. Railway on Free/Trial/Hobby plans, or DigitalOcean by default), so there the HTTPS API is the only option that works.

## How did you test this?

- Sent an invitation from the app image (working tree mounted) to a local Mailpit with `SMTP_SECURITY=none` and `RESEND_API_KEY` also set: the email arrived with the correct From/To/Subject and the accept link in the HTML part, and Resend was not called.
- `SMTP_SECURITY=starttls` against a server without TLS: `send_invitation_email` returns `False` and logs `STARTTLS extension not supported by server.`, so the existing Celery retry / FAILED flow applies.
- Unit tests for transport selection, starttls / ssl / none, optional login and connection errors.

Not tested against real SES, Azure or Resend accounts.

## AI usage

Claude Code (Claude Opus) for the implementation, tests and docs draft; reviewed and edited by me.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Email invitations can be sent through SMTP or Resend. Setting an SMTP host selects SMTP; otherwise, Resend is used. SMTP supports STARTTLS, SSL, or unencrypted connections, with optional authentication.
  * Invitation emails now include plain-text content.
* **Documentation**
  * Added SMTP setup instructions and examples, including security settings and a note that some hosting platforms restrict outbound SMTP.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `943a4b461d91`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.