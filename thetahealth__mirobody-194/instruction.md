# Issue

**Title:** user: a self-hosted server introduces itself as Mirobody

## Description

## Why

A self-hosted Mirobody presented itself under the hosted product's names in two places:

- With `EMAIL_FROM_NAME` unset (it is commented out in `config.yaml`), sign-in codes went out from **"Theta Wellness"**.
- With `WEBAUTHN_RP_NAME` unset, the browser offered to save a passkey for **"Theta Health"**.

## What changes

- Both defaults are now **"Mirobody"**.
- The sender default was written in four places. It is now set once, at the top of `create_email_validator`.
- `config.yaml` documents `EMAIL_FROM_NAME` and `WEBAUTHN_RP_NAME`.

Theta's hosted services do not run this auth code, so nothing they send changes. The WebAuthn RP name is display text only. The RP ID is what binds credentials, and it is untouched.

## Verified

- An SMTP validator built without `from_name` now carries "Mirobody", and an explicit name still wins.
- ruff, compileall and lint-imports (6 kept) pass.
- pytest: 1165 passed, 113 skipped, 12 xfailed.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `18bbe47183ee`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.