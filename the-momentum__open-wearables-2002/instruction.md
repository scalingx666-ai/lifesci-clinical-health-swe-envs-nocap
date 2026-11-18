# Issue

**Title:** fix(backend): refuse to seed a production admin with the default password

## Description

## What does this change?

Takes over #1815 by @slavarosin (the fork is owned by an organization, so maintainers can't push to its branch), rebased on current `main`.

`seed_admin.py` now refuses to create the admin in production when the password is still the config default (`your-secure-password`). It raises `DefaultAdminPasswordError`, and since `app.sh` runs with `set -e` the startup fails with a clear message instead of finishing. The default is now imported from `app.config` (`DEFAULT_ADMIN_PASSWORD`, added on `main` in the meantime) instead of being redefined in the script.

Also adds a short note to the `ADMIN_PASSWORD` row in `docs/deployment/docker.mdx`.

## Why?

If a production deployment forgets `ADMIN_PASSWORD`, it silently gets `admin@admin.com` / `your-secure-password`, which is public. The forced password change after login doesn't close this: whoever logs in first sets the new password.

The check sits after the "a developer already exists" return, so live databases with a developer are unaffected, and local/dev still works with the default. The Railway template already requires `ADMIN_EMAIL` / `ADMIN_PASSWORD`.

Related issue: supersedes #1815

## How did you test this?

- `tests/scripts/test_seed_admin.py` (4 tests) and `tests/api/v1/test_auth.py`: 48 passed. `ruff check`, `ruff format --check` and `ty check` clean.
- Ran the full `scripts/start/app.sh` in Docker on a fresh Postgres with `ENVIRONMENT=local` and the default password: admin is created, the app starts and login works.

## AI usage

Prepared with Claude Code, reviewed by me.

Co-authored with @slavarosin, original work in #1815.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Initial admin account creation in production now fails when the default password is used. Existing developer accounts are unaffected, and custom production passwords and the default local password continue to work.
* **Documentation**
  * Deployment guidance now clarifies that a custom admin password is required in production.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fd6fc899394d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.