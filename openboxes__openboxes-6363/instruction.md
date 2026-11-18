# Issue

**Title:** OBLS-1073 Answer 404 when dropping to an unknown staging location

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:** https://openboxes.atlassian.net/browse/OBLS-1073

**Description:**

When a picker drops a tote at a staging location that is not a location of the facility, `PATCH /api/facilities/{facilityId}/pick-tasks/containers/{outboundContainerId}` (`action: drop`) answered **500** with `Staging location does not exist`. The message did not say what was scanned, and a 500 reads as a server fault rather than a scanning mistake.

Now:

| Request | Before | After |
|---|---|---|
| `stagingLocationId` matches no location of the facility (by id or location number), including one that belongs to another facility | 500 `Staging location does not exist` | **404** `Staging location <value> not found` |
| `stagingLocationId` missing, null or blank | 500 `Staging location does not exist` | **400** `Staging location is required` |
| Everything else (location without STAGING_LOCATION / HOLD_STOCK, zone mismatch + override, empty tote, unknown action) | unchanged | unchanged |

The 404 matches what the same call already answers for an unknown outbound container. The mobile app shows a 404's `errorMessage` exactly as it showed the 500's (inline under the staging scan field, field cleared for a rescan), so no app change is needed.

Note on the ticket: it describes the app showing only a general error. With the current app build that is not the case - the app already showed the server's message, "Staging location does not exist", inline under the scan field (see the Before screenshot). A general error is what app builds older than the change that displays server error messages show for any 500, so that part of the report likely comes from an older build on the handhelds. This PR does not change what an older build displays; it makes the response a 404 and names the scanned value.

How:
- `PickTaskService.dropToStaging` throws a new `StagingLocationNotFoundException` (extends `IllegalArgumentException`, so other callers see the same exception type as before) for an unknown location, and an `IllegalArgumentException` for a blank one.
- `PickTaskApiController.drop` answers 400 for a blank `stagingLocationId` before calling the service, and catches only `StagingLocationNotFoundException` to answer 404. The exception is thrown before any write, and the service transaction rolls back.

Tests:
- `PickingContractSpec` (app-shaped HTTP calls): unknown value -> 404 with the value in the message; another facility's staging location by id and by location number -> 404; empty, whitespace, null and missing -> 400; drop by location number (what the scanner sends) succeeds; non-staging location, unknown action and empty tote keep their 500 and message. Every rejected drop is checked to change nothing: task status and staging fields, order status, tote stock, and transaction entries on the tote and the staging location.
- `PickTaskIntegrationSpec`: service-level message assertions updated (unknown, blank).
- `test/e2e/tests/mobile-api/picking.spec.ts`: unknown staging location -> 404 with the message.
- Ran `PickingContractSpec`, `PickTaskIntegrationSpec` and `TaskFacilityIntegrationSpec` locally on MySQL 8.0.36 and MariaDB 10.3.39 (PR CI runs the regression suite on MySQL only): all pass.

Not covered by a new test: the zone-mismatch path over HTTP. Testing it would require enabling `VALIDATE_STAGING_LOCATION_ZONE` on the shared regression facility. The change only catches the new exception type, so `StagingLocationMismatchException` still reaches its existing handler.

Possible follow-up, not in this PR: the other drop errors (location that is not a staging location, empty tote, unknown action) still answer 500 with a readable message. Moving them to 4xx would change the error contract for these calls more broadly.

---
### :camera: Screenshots & Recordings (optional)

Mobile app (current app build, no app change), Pick Staging Location step, scanning `NO-SUCH-LANE`, which is not a location of the facility:

| Before (500) | After (404) | After: rescanning the real staging location completes the pick |
|---|---|---|
| <img src="https://raw.githubusercontent.com/christianallen/openboxes/issue-assets/obls-1073-staging-location-before.png" width="280"> | <img src="https://raw.githubusercontent.com/christianallen/openboxes/issue-assets/obls-1073-staging-location-after.png" width="280"> | <img src="https://raw.githubusercontent.com/christianallen/openboxes/issue-assets/obls-1073-staging-location-after-rescan.png" width="280"> |

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `654afedcd800`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.