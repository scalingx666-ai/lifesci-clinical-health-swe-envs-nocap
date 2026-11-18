# Issue

**Title:** Add ClientApplication default access policy

## Description

## Summary

Adds a `ClientApplication` default access policy, tightens the `Bot` default to match it, and moves the default access policy definitions into one module.

## Changes

- **`ClientApplication` default.** New projects get a `Default ClientApplication Access Policy`. `createClient` applies it when no `accessPolicy` is passed, including for each new project's default client. It grants read/write on all
resource types except `AccessPolicy`, `Bot`, and `ClientApplication`, which are read-only. `ClientApplication.secret` and `retiringSecret` are hidden.
- **`Bot` default.** `Bot` and `ClientApplication` are now read-only as well (before, only `AccessPolicy` was). Bots can no longer modify Bots or ClientApplications.
- **`POST /admin/projects/:projectId/client`.** For super admins, the handler now reads the target project. Before, it passed a stub `Project`, so that project's defaults were never found. Other callers now get `403` for a project that
isn't their own; before, the client was quietly created in their own project.
- **Refactor.** Policy contents live in `DEFAULT_ACCESS_POLICIES` (`fhir/default-access-policies.ts`), and `projectinit` creates one policy per entry. `getDefaultAccessPolicy(project, profileType)` replaces the inline
`defaultAccessPolicies.find(...)` lookups in `invite`, `botinit`, `client`, and `reconcileDefaultAccessPolicy`. The Admin, Practitioner, Patient, and RelatedPerson policies are unchanged.
- **Schema and docs.** Adds `ClientApplication` to the `project-membership-profile-type` CodeSystem and to `ProjectDefaultAccessPolicies.profileType`. Updates the default access policy table and documents that clients with this default
can't deploy Bots.

## Policy construction

Access policy entries are additive, so a writable `*` can't carry read-only exceptions. When any non-admin type must be read-only, `writableExcept` emits a read-only `*` plus one writable entry per allowed type; otherwise it emits a plain
`*`. Entries with hidden fields come before the wildcard because the server takes `hiddenFields` from the first matching entry. `AccessPolicy` gets its own read-only entry because `*` never matches project admin types.

## Reviewer notes

- Only new projects are affected. Existing projects are not backfilled, so their clients and their existing Bot default policies stay as they are.
- A new project's default client can't save or deploy Bots (`Bot/$deploy` returns 403). CI/CD deploys need a client whose policy grants write on `Bot`.
- Like the Practitioner default, the Bot and ClientApplication defaults list writable types explicitly. Resource types added in later releases will be read-only under these policies until the policies are updated.
- A Bot or client membership with `admin: true` gets the project admin entries in place of the read-only `AccessPolicy` entry. `Bot` and `ClientApplication` stay read-only, and secrets stay hidden.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4d8621581b26`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.