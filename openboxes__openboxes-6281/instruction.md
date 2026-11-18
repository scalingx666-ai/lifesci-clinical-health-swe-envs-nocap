# Issue

**Title:** OBLS-1023 Defer status-only responses until the commit in API specs

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:**
https://openboxes.atlassian.net/browse/OBLS-1023 (completes #6262, the backport of #6183)

**Description:**

`StockMovementItemApiSpec` fails intermittently on unrelated changes. It failed twice on 2026-10-19: in CI on #6271 (regression integration shard 6, MySQL, "an item can be removed": after the 204 from removing the item, the item list still contained it, `StockMovementItemApiSpec.groovy:212`) and in a local MySQL run ("... have its pick reverted": after the 204 from reverting the pick, the picked quantity was still 3, `:107`). Both checks read the database right after a `render status: 204` in `StockMovementItemApiController`, which is transactional at the class level.

Cause: `render` with only a 2xx status ends with `response.flushBuffer()`, inside the action and so inside its transaction. That commits the headers, and a 204 has no body, so the client has the complete response as soon as the headers arrive - before the transaction has committed. The spec's next read can run before the commit. `DeferResponseCloseFilter` (#6262) holds back the writer and stream `close()` that JSON responses go through, but not `flushBuffer()`, so bodiless status-only responses were not covered. A status-only `200` is sent chunked and the client waits for the end of the response, and a status of 300 or more goes through `sendError`, which does not flush; that is why only the 204 sites are affected. Of the 23 `render status: 204` sites in the API controllers, three render inside the action's transaction today (the two in `StockMovementItemApiController` and `CategoryApiController.delete`).

Fix: the filter's response wrapper ignores `flushBuffer()` while the status is one Tomcat sends without a body (204, 205, 304). The container sends the response when the request finishes, after the action's transaction has completed. Status, headers and body bytes are unchanged; only the end of the response moves, as the filter already does for JSON responses. For every other status `flushBuffer()` is passed on as before. Test infrastructure only: no application code, no configuration, nothing packaged (the integration test source set is not in the WAR). `StockMovementItemApiSpec` itself stays as it is.

One intended consequence: a commit that fails after a bodiless status-only render now reaches the client as the error response, instead of a 204 that was never true. Before the change the 204 was already committed when the commit failed, so the error was lost.

## Tests

- `DeferResponseCloseFilterSpec`, two new features next to the existing writer-close feature, both on `DELETE /api/categories/{id}` (`CategoryApiController.delete`: the delete is flushed inside the action, then `render status: 204`). A Hibernate post-delete listener registers a transaction synchronization whose `beforeCommit` runs after the action has returned:
  - holds the commit: the client must still be waiting after 1 s; after release it gets the 204 and the category answers 404;
  - fails the commit: the client gets the JSON error response (500), not the 204, and the category is still there.

Run against the unchanged filter first, both new features failed as expected (the client had the 204 while the commit was held; the client got a 204 for the failed commit); both pass with the change, and fail again with 204 taken out of the deferred statuses. With the writer-close deferral removed instead, only the existing insert feature fails, so the features cover different paths.

## Verification

Run locally the way this branch's workflows run it (backend and regression workflows):

- Backend (`./gradlew jacocoTestReport`) on `TEST_DATABASE=mysql:8.0.36` and on `mariadb:10.3.39`: unit 1,510 tests, integration 72 tests (the two new features included), 0 failed on both.
- Regression suite (`./gradlew regressionTest regressionIntegrationTest`) on both databases: 2,433 unit and 1,248 integration tests, 0 failed on both. 66 and 272 skipped are the suite's pending features.
- `StockMovementItemApiSpec` run 10 times in a row on MySQL with the change: 11 tests, 0 failed in every run.
- This change touches no frontend file.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3d7b1c5744d1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.