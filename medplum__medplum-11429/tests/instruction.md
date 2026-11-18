# Issue

**Title:** feat(server): add per-client external auth callback path

## Description

ClientApplications with an `identityProvider` get their own external auth callback, `/auth/external/<clientId>`. The shared `/auth/external` callback keeps working for them only when their Project has the `legacyExternalAuth` system setting, which only super admins can set.

With a callback per client, the redirect URI registered at the identity provider identifies the client the authorization code was issued for. On the shared callback, the client is read from `state`.

DomainConfiguration and server-config (`externalAuthProviders`) identity providers are unchanged and keep using `/auth/external`.

## Changes

**New route `GET /auth/external/:clientId`** (`auth/routes.ts`, `auth/external.ts`)
- Uses only that client's identity provider, with no fallback to a DomainConfiguration or server-config identity provider.
- Returns `400 Invalid client` when `state.clientId` does not match the path.
- Sends the same per-client `redirect_uri` in the token request, as the identity provider requires.

**Shared callback requires `legacyExternalAuth` for client identity providers** (`auth/external.ts`)
- When `state.clientId` names a client with an `identityProvider`, `/auth/external` serves it only if the client's Project has `systemSetting` `legacyExternalAuth = true`.
- Otherwise it returns `400 Invalid redirect URI for client identity provider, use <baseUrl>auth/external/<clientId>`, before any request to the identity provider.
- Only `Project.systemSetting` is read. The same name in `Project.setting` has no effect.
- Clients without a Project (server config `defaultOAuthClients`, or created by a super admin) are always allowed.

**Logging** (`auth/external.ts`)
- Each successful sign-in through a client identity provider on the shared callback logs `Client identity provider signed in through the shared external auth callback` with `clientId` and `projectId`. This shows which Projects still need to migrate.

**Docs and example**
- The external identity provider docs and `packages/examples/src/auth/external-identity-providers.ts` now use `/auth/external/<clientId>` as the redirect URI.

## Behavior changes

- **New and unlisted Projects:** a ClientApplication identity provider must use `/auth/external/<clientId>`. Sign-ins through `/auth/external` fail with the 400 above.
- **Projects with `legacyExternalAuth`:** no change. `/auth/external` keeps working, and each sign-in is logged.
- **Self-hosted servers:** after upgrading, ClientApplication identity providers on `/auth/external` stop working until a super admin sets `legacyExternalAuth` on the Project, or the client is moved to the per-client callback.

## Migrating a client

1. Register `https://<server>/auth/external/<clientId>` as a redirect URI at the identity provider. `<clientId>` is the Medplum ClientApplication id.
2. Pass that URI as `redirectUri` to `MedplumClient.signInWithExternalAuth` (or as `redirect_uri` if you build the authorize URL yourself).
3. Remove `https://<server>/auth/external` from the identity provider's allowed redirect URIs.

No SDK upgrade is needed.

## Rollout

- On the hosted service, `legacyExternalAuth` is set on every Project with a ClientApplication identity provider that signed in through `/auth/external` in the last 30 days, before this deploys.
- Those Projects have 30 days to migrate. After that, `legacyExternalAuth` is removed.
- If an unlisted Project reports the new 400, setting `legacyExternalAuth` on it restores the old behavior without a deploy.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `237232ce2cc6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.