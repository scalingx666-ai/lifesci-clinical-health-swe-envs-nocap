# Issue

**Title:** chore(server): log memberships granted to existing users with unverified email

## Description

## Summary

When an invite (`POST /admin/projects/:id/invite`), or `Project/$init` with `ownerEmail`, matches an existing `User` by email address and that `User` has not verified the address (`emailVerified` is not `true`), log a warning. The log includes the user, project, membership, profile, `admin`, `invitedBy`, and source (`invite` or `project-init`). It is throttled per project and user over a 10-minute window with `LogThrottle`.

This change only logs. Invites and `$init` behave the same as before. Self-registered accounts are usually unverified, so requiring verification here right away would affect existing users who are invited to another project. The logs will show how often that happens before we choose an enforcement policy.

## Testing

- `admin/invite.test.ts`: inviting an existing unverified user logs once; inviting an existing verified user or a new address does not.
- `fhir/operations/projectinit.test.ts`: `ownerEmail` matching an existing unverified user logs with `admin: true`; a newly created owner does not.
- Both new assertions fail without the source change.
- `npx vitest run src/admin src/auth src/oauth src/scim src/fhir/operations/projectinit.test.ts` passes, except the sharding suite in `admin/super.test.ts`, which needs a local shard database. eslint, prettier, and `tsc --noEmit` are clean.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c956ffb66d65`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.