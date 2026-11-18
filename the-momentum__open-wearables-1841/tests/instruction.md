# Issue

**Title:** fix(backend): link SDK refresh tokens to the application that issued them

## Description

## What does this change?

`refresh_token.app_id` is replaced with an `origin` (`application` / `admin` / `invite`) plus real foreign keys: `application_id` → `application` (`ON DELETE CASCADE`) and `issued_by_developer_id` → `developer` (`ON DELETE SET NULL`). A check constraint keeps the combination consistent. The `app_id` claim in SDK access tokens keeps its current format.

## Why?

The column mixed real app IDs with `admin:{developer_id}` and `invite:{developer_id}` strings, so it couldn't have a foreign key. In practice this meant deleting an application didn't cut off its users: their refresh tokens kept rotating forever.

I kept `developer_id` for developer tokens only. Reusing it for the issuer of SDK tokens would make `get_by_developer_id` / `revoke_all_for_developer` pick them up too.

### Potential breaking change

The migration deletes SDK refresh tokens whose application no longer exists. Users of already-deleted applications will get a 401 on their next refresh and the SDK will report an auth error ([Handle expired sessions](https://openwearables.io/docs/sdk/integration#handle-expired-sessions)). This should go in the release notes. Admin/invite tokens whose developer was deleted stay valid, because removing a team member shouldn't log out end users.

To check whether an instance has such tokens, run this before upgrading:

```sql
SELECT rt.app_id,
       count(*) AS active_tokens,
       count(DISTINCT rt.user_id) AS users,
       max(coalesce(rt.last_used_at, rt.created_at)) AS last_activity
FROM refresh_token rt
LEFT JOIN application a ON a.app_id = rt.app_id
WHERE rt.token_type = 'sdk'
  AND rt.revoked_at IS NULL
  AND a.id IS NULL
  AND split_part(rt.app_id, ':', 1) NOT IN ('admin', 'invite')
GROUP BY rt.app_id
ORDER BY last_activity DESC;
```

Apps that handle the SDK auth error by getting new tokens from their backend and passing them to `updateTokens()` recover on their own, as long as that backend uses the credentials of an application that still exists.

## How did you test this?

Ran the migration on Postgres 16 seeded with rows in the old format:

| token | old `app_id` | after upgrade |
|---|---|---|
| live app | `app_live` | `origin=application`, `application_id` set |
| deleted app | `app_gone` | deleted |
| admin | `admin:<existing dev>` | `origin=admin`, issuer set |
| admin, dev deleted | `admin:<missing dev>` | `origin=admin`, issuer NULL |
| invite | `invite:<existing dev>` | `origin=invite`, issuer set |
| developer token | NULL | unchanged |

After that, `DELETE FROM application` removed the app's token, and `alembic check` showed no drift. The downgrade restores the old `app_id` strings.

## AI usage

Claude Code (Claude Opus) for the implementation, migration and the test run above; I reviewed the design and the diff.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Authentication**
  * SDK access and refresh tokens retain their application or developer issuance details when issued and refreshed.
  * Refresh tokens associated with an application are no longer valid after that application is deleted.
  * Invitation-issued tokens retain their invitation origin and issuing developer details.
  * Admin-issued SDK tokens retain their origin and issuing developer details when refreshed.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `456b82502fea`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.