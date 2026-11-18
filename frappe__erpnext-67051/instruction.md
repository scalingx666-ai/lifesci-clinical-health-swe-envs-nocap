# Issue

**Title:** fix(buying): check Request for Quotation write permission in send_supplier_emails (backport #65960)

## Description

Backport of #65960 to `version-15-hotfix`.

`send_supplier_emails` (the **Tools > Send Emails to Suppliers** button on a submitted Request for Quotation) loaded the document without a permission check. Before the later save refused the caller, it had already created portal users for supplier email addresses and sent their welcome emails. It now checks write permission on the Request for Quotation first, and accepts only POST requests.

**Fix:** call `rfq.check_permission("write")` after the Request for Quotation is loaded, and allow only POST requests. ()

**Changes compared with develop:** The decorator line conflicted, because the function has no type annotation on this branch. The signature of this branch is kept and only `methods=["POST"]` is added. The test file conflicted only because develop has other tests next to the new test. Only the new test is added. On version 15, `frappe.get_doc` does not support the `check_permission` argument (it ignores it), so the fix calls `rfq.check_permission("write")` on the next line instead. The test is placed before `test_get_pdf`, and the test of #67050 (email preview) is placed after it, so the two PRs do not change the same lines of `test_request_for_quotation.py`. Each PR merges on its own.

 for the example and the steps to test.

### Tests

- `test_send_supplier_emails_needs_write_permission`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_request_for_quotation.py` (complete file): all tests pass except `test_get_pdf`, which needs `wkhtmltopdf`. The test machine does not have it, and the test fails the same way on `version-15-hotfix` without this change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.