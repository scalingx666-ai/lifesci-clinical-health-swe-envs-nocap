# Issue

**Title:** fix(core): apply wildcard access policy criteria to single resources

## Description

An AccessPolicy entry with `resourceType: '*'` and criteria such as `*?_compartment=Patient/<id>` is applied consistently by search but not by single-resource checks.

- **Search** (`Repository.addAccessPolicyFilters`) rewrites `*?<params>` to `<searched type>?<params>` before building the SQL filter, so reads and searches are scoped as expected.
- **Single-resource checks** (`satisfiedAccessPolicy` in core) parsed `*?<params>` as a search on type `*`, and `matchesSearchRequest` rejects it because `*` never equals `resource.resourceType`. The entry never matched any one resource.

So with `*?_compartment=Patient/A`, a member could read and search A's Observations but got `Forbidden` on create, update and delete of them. The same gap affected everything else that goes through `satisfiedAccessPolicy` / `canPerformInteraction`: `hiddenFields` / `readonlyFields`, subscription and WebSocket notification checks, `$deploy`, `$set-accounts`, and the client-side helpers (`canWriteResource`, `ResourceForm`, `ResourceTable`). It also affected SMART `patient/*.xxx` scopes on a `*` membership entry, which narrow to `*?_compartment=Patient/<context>`.

## Changes

- `packages/core/src/access.ts`: when a `*` entry's criteria starts with `*?`, evaluate its parameters as `<resource.resourceType>?<params>`, matching the search path. Project admin resource types stay excluded from wildcards (unchanged `shallowMatchesResourcePolicy`). Criteria that don't start with `*?` are evaluated as before.
- A parameter that the resource's type does not define never matches (`matchesSearchFilter` returns false for unknown codes), so the entry doesn't apply to that resource and no error is thrown. For example, `*?status=final` covers final Observations but no Organizations. Search already rejects such a criteria with a 400 `Unknown search parameter` for types that lack the parameter. That behavior is unchanged.
- Tests:
  - Core matcher tests for `_compartment`, `_id`, `_lastUpdated`, `_tag`, `_security`, `_profile`, `_source` and `_project`, plus project admin types and unknown parameters.
  - Server tests for a member with `*?_compartment=Patient/A`:
    - create, update and delete of A's Observation are allowed;
    - B's Observation is refused, including moving A's Observation to B;
    - Organization and Bot are refused.
  - Server tests for `hiddenFields` on a `*` criteria entry, a `_tag` criteria, a SMART `patient/*.cruds` scope, and an unknown parameter.

## Compatibility

This changes what existing policies allow. Any `*` entry with `*?...` criteria now matches the individual resources its criteria select, where before it matched none. Specifically:

- **Writes are now allowed.** Create, update and delete succeed for resources that match the criteria and the entry's `interaction` / `readonly` settings. Before, they were refused.
- **Field rules now apply.** The entry's `hiddenFields`, `readonlyFields` and `writeConstraint` now apply to those resources. Before, reads returned hidden fields unredacted.
- **Earlier entries can now win.** `satisfiedAccessPolicy` returns the first matching entry, so a `*` criteria entry listed before a more specific entry is now selected for resources it matches. Its field rules then take precedence.
- **More notifications.** Subscription and WebSocket notifications for authors with such policies now deliver for matching resources.
- **SMART wildcard scopes.** `patient/*.c|u|d` scopes over a `*` membership entry now permit writes within the patient compartment.

## Testing

- `packages/core`: `npx vitest run src/access.test.ts src/search src/subscriptions src/elements-context.test.ts`: 8 files, 325 passed.
- `packages/server`: `npx vitest run` on `fhir/accesspolicy`, `fhir/repo`, `fhir/smart`, `fhir/search`, `workers/subscription`, `ws`, `auth`, `oauth`, `admin/invite`, `fhir/precommit`, `fhir/references`, `fhir/default-access-policies`, `fhir/repository/method-guards`, `fhir/projectmembership`, `fhir/operations/{botinit,groupexport,rescope,deploy}`, `openapi`, `webhook/routes`: 63 files, 1901 passed, 7 skipped.
- Without the `access.ts` change, 10 of the new core tests and all 5 new server tests fail.
- `eslint` and `prettier --check` pass on the changed files. `tsc --noEmit` is clean in `packages/core`. In `packages/server` it reports only the same 38 stale `@medplum/ccda` dist errors seen on `main`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cd70174b821a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.