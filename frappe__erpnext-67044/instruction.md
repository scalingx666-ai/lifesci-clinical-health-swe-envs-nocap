# Issue

**Title:** fix(buying): sanitize the Request for Quotation email preview (backport #65951)

## Description

Backport of #65951 to `version-16-hotfix`.

The **Preview Email** dialog of a Request for Quotation added the rendered supplier message to the page as raw HTML. With **Use HTML** on, **Message for Supplier** is a Code field that is not cleaned on save, so event handlers in it were active in the dialog. The preview is now passed through `sanitize_html` before it is returned, so formatting stays and event handlers and scripts are removed.

**Fix:** pass the preview message of `get_supplier_email_preview` through `frappe.utils.html_utils.sanitize_html`. ()

**Changes compared with develop:** The import line conflicted because the imports above it are different on this branch. Only the `sanitize_html` import is added. The new test is placed after `test_get_pdf`, not before it as on develop, so that this PR and #67045 (`send_supplier_emails`) do not change the same lines of `test_request_for_quotation.py`. Each PR merges on its own.

 for the example and the steps to test.

### Tests

- `test_email_preview_keeps_formatting_and_drops_event_handlers`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_request_for_quotation.py` (complete file): all tests pass except `test_get_pdf`, which needs `wkhtmltopdf`. The test machine does not have it, and the test fails the same way on `version-16-hotfix` without this change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427f7f719f44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.