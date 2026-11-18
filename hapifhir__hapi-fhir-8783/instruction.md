# Issue

**Title:** In-memory `:in` / `:not-in` reports "not supported" when `ValueSet` membership cannot be decided

## Description

Part of #8415. 

### Problem
`InMemoryResourceMatcher` treated a code it could not check as outside the ValueSet, so a `:not-in`
match succeeded and `AuthorizationInterceptor` rules using `withFilter("code:not-in=...")` allowed reads they should have denied. This happened when the ValueSet uses a CodeSystem the server does not have (since #8427, unreleased) and when no validation support module answers for the `ValueSet`, for example when the server does not have it (since #3680, in every release from 6.1.0).

### Changes

- `InMemoryResourceMatcher`: when a code cannot be checked against the ValueSet, an in-memory `:in` / `:not-in` match
  is now unsupported instead of a match or no match:
  - HAPI-3066 names the `CodeSystem` the server does not have;
  - HAPI-3070 names the `ValueSet` no validation support module answered for.
- Effect on callers of the in-memory matcher:
  - `AuthorizationInterceptor` `withFilter` rules: an allow rule no longer applies, a deny rule does;
  - Subscriptions: fall back to a database search;
  - Bulk Export post-fetch filters: leave the resource out;
  - conditional create/update verification (`BaseHapiFhirDao:908`): skips the check instead of rejecting the request.
    Not in the changelog; decide whether to add it.
- Changelog `9_0_0/8415-authorization-valueset-rules-deny-unresolved-codesystem.yaml`: extended to `withFilter` rules and Subscriptions, for both an unknown CodeSystem and a ValueSet the server does not have; it says that before, a `:not-in` filter on a ValueSet the server does not have matched every code and let reads through.
- `validation_support_modules.md`, "ValueSets That Use an Unknown CodeSystem": one paragraph on how in-memory `:in` / `:not-in` behave when membership cannot be checked.

### Testing

- `InMemoryResourceMatcherR5Test`, two parameterized tests, each run for `:in` and `:not-in` (4 cases):
  - unknown CodeSystem → unsupported, HAPI-3066;
  - no validation result → unsupported, HAPI-3067.
- New `AuthorizationInterceptorValueSetFilterR4Test`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2b8f0e703697`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.