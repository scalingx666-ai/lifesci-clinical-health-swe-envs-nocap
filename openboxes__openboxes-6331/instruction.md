# Issue

**Title:** OBPIH-8092 Render notification emails in the current request instead …

## Description

…of PageRenderer

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:**

**Description:**
### Problem
After the Grails 7 migration, sending a shipment fails, for example Send shipment on an inbound stock movement (`POST /api/stockMovements/:id/status`). Completing a receipt fails the same way. Both end with:

    GrailsTagException [views/email/_shipmentShipped.gsp] <g:applyLayout> ...
    UnsupportedOperationException: You cannot use the session in non-request rendering operations

During the migration, `NotificationService.renderTemplate` was switched from `new RenderTagLib().render(...)` to `PageRenderer`. `PageRenderer` always renders in a synthetic request, and that request throws on `getSession()` and `getScheme()`. The email templates need both:
- `session` is read by `warehouse.message` (locale via `LocaleManager`/`SessionManager`) and directly (`session.warehouse` in `_shipmentReceived.gsp`).
- `scheme` is read by `createLink(absolute: true)`, because `grails.serverURL` is not configured.

The shipment status listener runs synchronously inside the transaction. The rendering error therefore rolls back the whole send or receive operation, not just the email.

### Fix
Restore the Grails 3 behaviour of `renderTemplate`:
- Render through the `g` dispatcher of the `gspTagLibraryLookup` bean. This is the same `TagOutput.captureTagOutput(...)` call that `new RenderTagLib().render(...)` compiled to in Grails 3. The `RenderTagLib` bean renders the template, and the output goes to a buffer, not to the HTTP response.
- Inside a request, the template sees the user's session, locale and host, as before the migration.
- Outside a request (for example in jobs), a mock request is bound with `GrailsWebMockUtil`, as in Grails 3. The only difference: the mock is now unbound in `finally`, so it no longer stays on the worker thread.

---
### :camera: Screenshots & Recordings (optional)

[//]: <> (If this PR contains a UI change, consider attaching one or more screenshots or recordings to help reviewers visualize the change. Otherwise, you can remove this section.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bfd46d6272cd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.