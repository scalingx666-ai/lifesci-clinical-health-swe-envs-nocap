# Issue

**Title:** enhance(email): tighten project SMTP transport setup

## Description

### TLDR

Project SMTP set up its transport from the raw configured host and used nodemailer's long default timeouts. This PR opens project SMTP connections through a `getSocket` hook that resolves the host once, fails fast on hosts that do not resolve to a usable address, lets the connection use any resolved address, and bounds the whole connect within `connectionTimeout`. Invite failures keep their response text and log the transport detail on the server.

### Prior State Analysis

- `sendEmailViaSmtp` passed `smtpHost` directly to nodemailer, which resolved it on its own and used default timeouts of 2 min to connect, 30 s for the greeting, and 10 min for an idle socket.
- A host that resolved badly surfaced as a late send failure, not a configuration error.
- The invite endpoint copied the transport error string into its response.

### Current Implementation State Analysis

Project SMTP now opens its socket through a nodemailer `getSocket` hook. The hostname stays the transport `host`, so TLS checks are unchanged. The server-wide SMTP and SES paths are unchanged.

- **`packages/server/src/email/`: project SMTP transport.**
  - `utils.ts` adds `getProjectSmtpSocket`, a `getSocket` hook. It resolves the host once, requires every resolved address to be usable, and hands the full address list to `net.connect` with `autoSelectFamily`, so the connection falls back across addresses. Resolving and connecting are bounded by `connectionTimeout`. A rejected host reuses the existing `Project SMTP is misconfigured` log and `Project SMTP configuration is incomplete or invalid` 400. IP literals are checked directly because `net.connect` skips the lookup for them.
  - `email.ts`: for project SMTP only, `sendEmailViaSmtp` installs the hook (unless `allowUnsafeOutbound` is set) and sets 20 s connection and greeting timeouts and a 2 min socket idle timeout. The failure log is unchanged.
- **`packages/server/src/admin/invite.ts`**: the send-failure outcome no longer includes `diagnostics`; the error is logged as `Invite email failed`. `details.text` and the 200 status do not change.
- **Tests**
  - `email/utils.test.ts` covers the hook: rejected hosts (including IP literals and mixed address sets), fallback to a second address when the first refuses, lookup errors, and the connect timeout.
  - `email/email.test.ts` covers the transport options, the `allowUnsafeOutbound` bypass, and the unchanged server SMTP options.
  - `admin/invite.test.ts` gains one assertion.

### Tests Completed to Verify Functionality

- `npx vitest run src/email src/admin/invite.test.ts src/auth/resetpassword.test.ts`: 5 files, 142 tests passing.
- `npx tsc --noEmit` (server), eslint, and prettier are clean on the touched files.
- Not yet verified: a live send through a hosted SMTP provider on 587 (STARTTLS) and 465 (implicit TLS).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `35f70cf8e436`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.