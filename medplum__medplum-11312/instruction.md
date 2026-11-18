# Issue

**Title:** fix(server): store a TOTP enrollment offer only when its login confirms it

## Description

## Changes

- TOTP enrollment offers (`POST /auth/login`, `GET /auth/login/:login`, and `GET /auth/mfa/status`) now each carry a secret that belongs to the login or session that received them. Repeated reads within 20 minutes return the same secret.
- `POST /auth/mfa/login-enroll` and `POST /auth/mfa/enroll` check the code against that login's offer, then store it as `User.mfaSecret` and end the offer. Previously, every offer returned the user's stored `mfaSecret`, and enrollment kept it.
- At login, `verifyMfaToken` enrolls the user before it marks the Login as verified. The User is written with `ifMatch`, so if two logins enroll at the same time, the second one gets `Already enrolled` and its Login is not verified.
- Offers are stored with one `SET … NX GET` call, so repeated reads return the same secret.
- `POST /auth/mfa/verify` only checks the stored authenticator secret when TOTP is an enrolled method. Before, it also checked it for users enrolled in email only or not enrolled at all. For a user who is not enrolled, a code for the login's own offer enrolls the user, as `/auth/mfa/login-enroll` does.
- Invites with `mfaRequired` no longer pre-generate an `mfaSecret`.
- `MfaPage` fetches the QR code again after a failed authenticator enrollment, so an expired offer is replaced without a reload.
- Docs: `auth/how-mfa-works.md` and `auth/mfa/index.md` updated. The invite docs (`app/invite/index.md`, `api/project-admin/invite.md`) no longer say an MFA secret is generated on invite.

## Compatibility

- An offer must be confirmed by the same login or session within 20 minutes. After that, enrollment returns `Secret not found` and the QR code must be fetched again. A QR code shown to one login, tab or device cannot confirm enrollment on another.
- Clients that confirm an enrollment offer with `/auth/mfa/verify` instead of `/auth/mfa/login-enroll` keep working, and the user is now enrolled in TOTP. Previously the login was granted but the user stayed unenrolled.
- Users enrolled in email only can no longer use authenticator codes unless they enroll TOTP.
- Users already enrolled in TOTP, including legacy users with `mfaEnrolled` and no `mfaMethod`, are unaffected and keep their secret.
- To provision a TOTP seed directly on a User, also set `mfaEnrolled: true` and `mfaMethod: ['totp']`.

## Testing

- New server tests:
  - Each login and session is offered its own stable secret.
  - Only the confirming login's secret is stored.
  - When two logins enroll at the same time, one wins, and the other gets `Already enrolled` with its Login left unverified.
  - Other offers are rejected at `/verify` after enrollment.
  - `/verify` ignores a stored secret for users who are not enrolled or are enrolled in email only.
  - `/verify` with a code for the login's own offer enrolls the user.
  - An expired offer returns `Secret not found`.
- New app test: a failed authenticator enrollment re-fetches `/auth/mfa/status`.
- Existing MFA tests adjusted where they took the secret from `/auth/mfa/status` and confirmed it from a different login.
- `auth`, `oauth` and `admin` server suites, plus `MfaPage` tests, pass. `tsc`, `eslint` and `prettier` are clean.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cc76f205d8bd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.