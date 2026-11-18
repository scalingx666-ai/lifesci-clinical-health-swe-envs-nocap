# Issue

**Title:** Add Bot default access policy

## Description

## What

Follows the pattern from #9724 (Admin/Practitioner defaults) to add a default access policy for Bots.

- **Project creation** (`projectinit.ts`): provisions a `Default Bot Access Policy` in the same transaction as the other defaults, and adds a `{ profileType: 'Bot' }` entry to `Project.defaultAccessPolicies`. The policy is full access except:
  - `AccessPolicy` is read-only (the `*` wildcard never matches project admin resource types, so this explicitly grants read).
  - `ClientApplication.secret` and `retiringSecret` are hidden fields, so Bots can't read or overwrite them.

  Hidden fields come from the first matching entry, so the specific entries are listed before `*`.
- **Bot creation** (`botinit.ts`): `createBot` falls back to the project's `Bot` default when no `accessPolicy` is passed. An explicit policy still wins. Covers both `Bot/$init` and the admin create-bot route.
- **Schema**: adds `Bot` to the `project-membership-profile-type` CodeSystem and to `ProjectDefaultAccessPolicies.profileType` in fhirtypes.
- **Docs**: adds a `Bot` row to the Default Access Policies table.

## Reviewer notes

- Existing projects are not backfilled; their Bots keep current behavior unless a `Bot` entry is added to `defaultAccessPolicies`.
- No admin-style reconciliation is needed for Bots, since nothing toggles a Bot between roles.
- A Bot whose membership has `admin: true` gets the project admin `AccessPolicy` entries, which replace the read-only one. New Bots are not admins.
- Tests added/updated in `botinit.test.ts` and `projectinit.test.ts`, including a test that loads the provisioned Bot policy and checks the AccessPolicy and ClientApplication restrictions. These have not been run locally (no Postgres/Redis available), so CI is the first run. Lint and Prettier pass.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1be16d64dd9c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.