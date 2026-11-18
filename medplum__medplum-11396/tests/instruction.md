# Issue

**Title:** fix(server): only super admins can set Bot.system

## Description

Only super admins can set or change `Bot.system`. For everyone else, `system` is a readonly field on `Bot` in the access policy built at login, so a write keeps the stored value: the flag is dropped on create and kept from the existing version on update and patch.

## Changes
- `getAccessPolicyForLogin` (`fhir/accesspolicy.ts`): for memberships outside super admin projects, `system` is made readonly on every entry that can write a `Bot`. This runs after SMART scopes, so entries narrowed from scopes are covered too.
  - An explicit `Bot` entry gets `system` added to its `readonlyFields`, unless it already lists `system` as readonly or hidden.
  - A `*` entry gets a `Bot` entry with the same fields (criteria rewritten from `*?` to `Bot?`, as search already does) plus `system` inserted ahead of it, since the first matching entry applies.
- Search (`fhir/repo.ts`): access policy criteria that another entry already applied are skipped, so a `*` entry and its `Bot` copy add one filter to a `Bot` search instead of two.
- `execute.test.ts`: `setupBot` sets `system` with the project system repository instead of a project admin token.

## Compatibility
Writes that include `Bot.system` from users outside super admin projects no longer change it, and no error is returned. Existing `system: true` bots are unchanged, and later edits keep the flag. The access policy returned by `/auth/me` includes the added `Bot` entries.

This should merge with or after #11406. On `main`, a `*` entry with criteria never matches a single resource, so the `Bot` copy of it would allow writes to Bots that the original entry does not. With #11406, the two entries match the same Bots.

## Testing
- New tests in `accesspolicy.test.ts`:
  - With no access policy, a `*` policy, a `Bot` policy, as a project admin, and with SMART scopes (`user/Bot.cruds`, with and without wildcard criteria), create, update and patch leave `system` unset; a super admin can set it; later edits keep it.
  - The policy shape: a `Bot` entry ahead of each `*` entry, with and without criteria; none for policies without `Bot` or `*`; and no change to entries that already protect `system`.
  - A `Bot` search under a `*` entry with criteria applies the criteria once.
- `npx vitest run src/fhir` plus `src/bots`, `src/cds`, `src/auth`, `src/oauth`, `src/admin`, `src/ws` and `workers/subscription`: all pass except suites that need a local shard database (`admin/super` sharding, `repository-connections`, `routing`, `db-configure-indexes`), which fail the same way on `main`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cc94a65b2e48`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.