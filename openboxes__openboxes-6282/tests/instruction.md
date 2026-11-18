# Issue

**Title:** OBLS-1020 Align role rules and facility checks for the warehouse task APIs

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:**
https://openboxes.atlassian.net/browse/OBLS-1020 (related: OBLS-952, OBLS-1019)

**Description:**

Gives the warehouse APIs this branch added the same role and facility rules as the rest of the application.

**1. Role rules.** `RoleInterceptor` takes the minimum role of an action without a rule from its name (`update...`, `save...`, `delete...` and so on need Assistant; anything else Browser). Names such as `allocate`, `patch`, `drop`, `rollback` or `printLabel` match none of those prefixes, so these actions only needed Browser. They now have explicit rules in `openboxes.security.rbac.rules` (`runtime.groovy`):

| Actions | Minimum role |
|---|---|
| Pick task `patch`, `reallocate`, `drop`; putaway task `patch` | Assistant |
| `allocationApi.allocate/deallocate` (`/api/requisitions/{id}/allocate`, `/deallocate`), `outboundOrderApi.allocate`, `allocation.allocate/deallocate/redoAutopick`, `stockMovement.allocate/clearPicklist/redoAutopick` | Manager |
| `stockMovementApi.packingLocation`, the three `printLabel` actions (product, container, bin location), `putaway.rollback/rollbackAndDelete`, `stockMovement.rollbackAndDelete`, `partialReceiving.autoreceive`, `requisition.issue` | Assistant |

The product, inventory level and location upserts are not changed here; the integration API work covers them.

**2. Facility checks on the pick and putaway task endpoints.** These URLs carry the facility (`/api/facilities/{facility}/pick-tasks/...`, `/putaway-tasks/...`), but tasks were looked up by id alone. Now:

- the user must hold a role at the facility in the URL, globally or at that facility (Browser to read, Assistant to change); otherwise 403. This does not depend on the location the session is logged into;
- a task of another facility is not found (404), also for `reallocate` and `alternate-destinations`;
- search, counts and routing suggestions use the facility of the URL;
- the bins a request names must belong to the task's facility: the tote of a pick (by id or location number), the staging lane of a drop, the bins of a reallocation, the cart of a putaway load and the destination of a putaway complete.

**3. Who did it.** The signed-in user is recorded as picked by, staged by and completed by; `pickedById`, `stagedById` and `completedBy` in the request are ignored. A task can still be assigned to a named user (`assigneeId` when starting a pick task, `assignee` when assigning a putaway task): to yourself as before, to someone else only with the admin role at the task's facility, as for reassigning the picker of an order (OBLS-952). An unknown user is refused.

Smaller changes that come with it:

- assigning a putaway task to a user without naming a cart no longer fails; an unknown cart id is refused;
- `GET .../putaway-tasks/{id}` answers 404 for an unknown task (it answered 200 with `data: null`), and an unknown tote on a drop answers 404 (it answered 500).

Compatibility: the mobile app chooses its location after signing in and sends its own user id as assignee, picker and stager, so pickers and putaway workers with the Assistant role (globally or at their facility) keep working; users who only have the Browser role can no longer change tasks or print labels. A user with the Manager role can still allocate and deallocate requisitions through the API. Nothing changes for administrators.

## Tests

- `UserServiceRoleAtLocationSpec` (unit, 8): the new `UserService.isUserInRoleAtLocation` - global roles count everywhere, a location role only at its location, higher roles count for lower ones, supplementary roles do not count, and the session's location plays no part.
- `WarehouseActionRoleSpec` (regression suite, 25): every action in the table called as Browser, Assistant, Manager and Admin (ids that do not exist, so nothing changes): every role below the minimum is refused, every role at or above it gets through; the rule of each action in `openboxes.security.rbac.rules`; a role held at the signed-in facility counts like a global one.
- `TaskFacilityIntegrationSpec` (regression suite, 13): a worker with the Assistant role at one facility reads, starts, picks and completes that facility's tasks and is recorded as the actor; the same tasks are not found through another facility's URL (also for an administrator), and are refused to a worker without a role at the facility; outbound containers, reallocation bins and putaway destinations of another facility are refused; assigning to another user needs the admin role at the task's facility; a Browser reads but cannot change; an unknown facility is not found; signing in without a location.
- Regression suite updates: the picker and stager in `PickTaskIntegrationSpec` and `RequisitionWebhookEventsIntegrationSpec` are now the signed-in user; a pick without a tote now reports that the tote does not exist; the pending feature "assign with only an assignee sets the assignee and keeps the task" (`PutawayTaskIntegrationSpec`) now passes and is no longer marked pending.

## Verification

Run locally the way this branch's workflows run it (backend and regression workflows):

- Backend (`./gradlew jacocoTestReport`) on `TEST_DATABASE=mysql:8.0.36` and on `mariadb:10.3.39`: unit 1,544 tests, integration 70 tests, 0 failed on both.
- Regression suite (`./gradlew regressionTest regressionIntegrationTest`) on both databases: 2,433 unit and 1,291 integration tests, 0 failed on both. 66 and 271 skipped are the suite's pending features.
- This change touches no frontend file.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c251bff2a015`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.