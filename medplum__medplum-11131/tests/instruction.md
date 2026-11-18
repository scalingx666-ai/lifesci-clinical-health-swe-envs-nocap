# Issue

**Title:** fix(server): limit the email API to the documented MailOptions

## Description

The `/email/v1/send` route now builds the nodemailer options from the `MailOptions` properties documented in `@medplum/core`, rather than passing the request body through to nodemailer. This keeps the API surface aligned with the documented type and with the sender and transport settings the server already manages.

## Changes
- `email/routes.ts`: copy `from`, `sender`, `to`, `cc`, `bcc`, `replyTo`, `subject`, `text`, `html`, `attachments` and `icalEvent` from the request. Attachments keep `filename`, `content`, `path`, `contentType`, `contentDisposition`, `cid` and `encoding`.
  - Content fields must be strings (or `false` for an attachment `filename`); other types return 400.
  - Other options are ignored and logged with their names.
- `core/src/client.ts`: document attachment `contentDisposition`, `cid` and `encoding`, add `MailIcalEvent` and `MailOptions.icalEvent`, and note which options the server uses.
- `email/routes.test.ts`: supported options, ignored options, invalid types, and the SMTP transport path.

## Compatibility
Requests using the documented `MailOptions` fields are unaffected. Requests that set other nodemailer options, such as custom `headers`, `inReplyTo` / `references` or `priority`, still send, but without those options. A warning is logged so they can be identified.

## Testing
- `npx vitest run src/email/`: 58 passed

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `96d19bef8972`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.