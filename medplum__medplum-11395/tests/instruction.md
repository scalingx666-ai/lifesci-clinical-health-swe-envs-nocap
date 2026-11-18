# Issue

**Title:** feat(server): support resending subscriptions for a specific resource version

## Description

## Summary

Adds a versioned `$resend` route so admins can replay the original subscription event for a historical resource version:

```
POST /fhir/R4/:resourceType/:id/_history/:vid/$resend
{ "subscription": "Subscription/...", "interaction": "update" }
```

Motivation: after an outbound delivery outage, rest-hook deliveries that exhaust their retries are not replayed. The existing instance-level `$resend` only resends the *current* version, so it cannot faithfully replay events for resources that have since changed, and it cannot replay deletes at all.

## Changes

- `ResendSubscriptionsOptions` gains `versionId` (set from the URL `:vid`; the instance route ignores a body `versionId`).
- **Authorization vs. content:** the caller's `readVersion` / `readHistory` performs the access checks; the versions used for evaluation are then loaded with `getSystemRepo().readVersion`, the same way `execSubscriptionJob` loads the delivered payload. This keeps `meta.project` and evaluates criteria against the delivered payload (including access-policy hidden fields).
- **Update:** the previous version (`%previous`) is the entry before `:vid` in resource history, found by paging `readHistory`. The same subscriptions match as for the original event.
- **Create:** evaluated without a previous version, as for the original create.
- **Delete:** the newest history entry must be the delete (412 otherwise); the server sends the last version before it, so delete works on the instance route without a version. If `:vid` is given it must match (400 otherwise). `%previous` is the deleted resource, matching `deleteResource`.
- No new SQL in `repo.ts`; only existing read paths are used.
- Docs: the `$resend` page covers the versioned route, create/update/delete behavior, and limitations.

## Known limitations (documented)

- A historical version gets one delivery attempt: the worker skips retries once the resource has changed since that version.
- `create`/`update` replays are not delivered if the resource has been deleted since.

## Testing

- `src/fhir/resend.test.ts`: historical update/create/delete, `%previous` evaluated against the version before it (including across history pages), delete `%previous` matching the original delete, subscription filter, non-extended mode, access-policy hidden fields, and error cases.
- `routes.test.ts`: versioned route over HTTP without the extended header asserts a job is queued; 404 unknown version; 403 non-admin.
- `routes.test.ts`, `workers/subscription.test.ts`, `method-guards.test.ts` pass locally.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e7e7e4019144`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.