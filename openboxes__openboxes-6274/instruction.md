# Issue

**Title:** OBLS-1019 Port develop's user role update checks to the branch

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:**
https://openboxes.atlassian.net/browse/OBLS-1019 (follow-up to OBLS-767)

**Description:**

Brings develop's #5948, #5960 and #5961 (user role permission handling, editing supplementary roles, and password changes for users below manager) to this branch. The OBLS-767 merge took develop as of 8 June; all three reached develop with the 0.9.8 release on 12 June, so the branch does not have them yet.

Four commits:

1. `git cherry-pick -x 788cace0a` (#5948), with upstream's specs (`RoleInterceptorSpec`, `UserServiceRoleValidationSpec`, `UserControllerSpec`).
2. `git cherry-pick -x 0e89fe06b` (#5960), with upstream's spec changes (`RoleSpec`, `UserServiceRoleValidationSpec`).
3. `git cherry-pick -x 17a864708` (#5961), with upstream's spec changes (`RoleInterceptorSpec`, `UserServiceRoleValidationSpec`). Without it, users below manager could not open their own user page to change their password.
4. Two specs for the role changes a request can make:
   - `UserServiceRoleUpdateSpec`: role changes through `UserService.updateUser`, both as requested role ids and as location role pairs. A user cannot grant or remove a role above their own highest role, a user below Assistant cannot change roles at all, and the target user's roles are left unchanged; granting a role at or below their own level still works.
   - `UserControllerRoleParamsSpec`: `update` and `save` pass a `roles` list to the service as the requested roles, and remove every other `roles...` and `locationRoles...` parameter before binding.

The three cherry-picks applied in order without conflicts and without hand edits; authorship is kept. The branch's own role types (Putaway and the discrepancy and stock transfer notification roles) fit the same rule, which compares each role's sort order.

## Tests

- Upstream's `RoleInterceptorSpec`, `UserServiceRoleValidationSpec`, `RoleSpec` and `UserControllerSpec`.
- `UserServiceRoleUpdateSpec` (27): 19 changes a user may not make (an Assistant, Manager or Admin granting a higher role to themselves or another user, globally or at a location, or removing a higher role; a Browser changing any role) and 8 they may.
- `UserControllerRoleParamsSpec` (3).

## Verification

Run locally the way this branch's workflows run it (backend, regression and frontend workflows):

- Backend (`./gradlew jacocoTestReport`) on `TEST_DATABASE=mysql:8.0.36` and on `mariadb:10.3.39`: unit 1,337 tests, integration 69 tests, 0 failed on both.
- Regression suite (`./gradlew regressionTest regressionIntegrationTest`) on both databases: 2,433 unit and 1,245 integration tests, 0 failed on MariaDB; on MySQL one `StockMovementItemApiSpec` feature ("an item can be picked automatically, cleared, picked by hand, and have its pick reverted") failed once and passed when the spec was rerun - it reads the database right after the response, which is a known intermittent failure unrelated to this change. 67 and 272 skipped are the suite's pending features.
- This change touches no frontend file.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ce62b6482839`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.