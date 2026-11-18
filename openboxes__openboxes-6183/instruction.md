# Issue

**Title:** Fix flaky API specs racing transactional controller commits

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:** No issue - follows the discussion in  about `run-backend-tests` failing intermittently.

**Symptom.** The API integration specs fail intermittently on unrelated branches and on both database legs. Two varieties, always on an entity that the immediately preceding request created and returned with HTTP 200:

```
POST /api/products -> 500
SQL Error: 1452 ... Cannot add or update a child row: a foreign key constraint fails
  (`test`.`product`, CONSTRAINT `FKED8DCCEFEF4C770D` FOREIGN KEY (`category_id`) REFERENCES `category` (`id`))
```

```
POST /api/facilities/1/inventory/record-stock/save -> 400
object references an unsaved transient instance - save the transient instance before flushing:
  org.pih.warehouse.product.Product
```

Recent examples: run 35123434333 (PR #6088, mysql), 35097615171 and 35004180773 (mysql), 35007654990 (mariadb). `ApiSpec.setup()` creates a category and a product through the API before every test, so every API spec is exposed. Which tests fail depends on runner load.

**Cause.** `grails.converters.JSON.render(HttpServletResponse)` ends with `writer.flush(); writer.close()` on the servlet response writer. Closing the writer makes the container finish the response, so the client sees a complete response at that point. In a controller annotated with `@Transactional` at the class level - `CategoryApiController` and `ProductApiController` among them - `render ... as JSON` runs inside the transaction, and the INSERT is flushed and committed only when the action returns. The specs fire their next request the moment the previous response completes, so that request can reach the database before the commit. Locally the commit wins by milliseconds; on a loaded runner it loses a few percent of the time per request.

Deterministic reproduction: add `Thread.sleep(500)` after `render category.toJson() as JSON` in `CategoryApiController.save()` and run `RecordStockApiSpec` - all three tests fail with the FK error above, because every product POST arrives while the category thread is still sleeping inside its uncommitted transaction.

**Fix (test infrastructure only).** `DeferResponseCloseFilter`, a servlet filter that lives in `src/integration-test/groovy` and is registered for every integration spec from `IntegrationSpecConfig`. It wraps the response so that `close()` on the response writer or output stream flushes what was written and then discards further output (as the container does after a real close) but does not close the underlying stream. The container completes the response when the request finishes - after the controller action has returned and its transaction has committed - so a spec's next request can no longer overtake the previous request's commit. Status, headers and body bytes are sent exactly as before; only the end of the response moves. `reset()` drops the cached wrappers so the servlet contract for switching between writer and stream is preserved.

Nothing under `grails-app/` or `src/main/` changes, and the filter is not compiled into the WAR. The same window exists for real clients (create, then immediately fetch), which is worth a separate conversation about where transactions should live; this change only makes the suite deterministic.

Alternatives considered: `save(flush: true)` in the two setup controllers turns the FK error into a lock wait and does not help the record-stock version of the issue; retrying in the test client would mask the cause.

**Tests.** `DeferResponseCloseFilterSpec` registers a test-only Hibernate post-insert listener that blocks the commit of a category save after the INSERT is flushed - i.e. after the controller has rendered - posts the category on another thread, and asserts that the HTTP client is still waiting while the commit is blocked, then completes once it is released and can read the category back. Without the filter the assertion fails (the client completes as soon as the converter closes the writer). The listener is restored to the original set in `cleanupData()`.

**Verification.**
- `DeferResponseCloseFilterSpec` fails on `develop` without the filter and passes with it.
- `RecordStockApiSpec` with the sleep reproduction above still applied: 3/3 fail without the filter, 3/3 pass with it.
- Same two specs on Jetty 9.4.19 (`-PWEB_SERVER=jetty`): 4/4 pass.
- Non-JSON paths with the filter in place: a decorated GSP page, a CSV rendered with `render(contentType:, text:)`, a save-then-redirect in a class-level `@Transactional` controller followed immediately, the 404 page and the 500 page all arrive complete.
- Full backend suite (`./gradlew jacocoTestReport`, the CI command) with the filter registered for every integration spec: MySQL 8.0.36 and MariaDB 10.3.39 both green - 1508 passed, 0 failed, 13 skipped on each.
- `DeferResponseCloseFilter*.class` appears only under `build/classes/groovy/integrationTest`, not under the main class output.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b500f168d7a5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.