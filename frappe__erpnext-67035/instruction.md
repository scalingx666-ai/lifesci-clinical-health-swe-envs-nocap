# Issue

**Title:** fix(stock): escape the warehouse name in the Batch stock levels (backport #65965)

## Description

Backport of #65965 to `version-16-hotfix`.

The **Stock Levels** section of the Batch form put the warehouse name into the HTML of each row and of the **Move** and **Split** buttons without escaping. A warehouse name with a double quote broke out of the `data-warehouse` attribute. The warehouse name is now escaped with `frappe.utils.escape_html`.

**Fix:** Escape the warehouse name once and use it in the row text and in both `data-warehouse` attributes. ()

**Changes compared with develop:** None. The commit applies without changes.

 for the example and the steps to test.

### Tests

- JavaScript only, so there is no Python test. A node script loads `batch.js` with a stubbed `frappe`, renders the Stock Levels row for a warehouse whose name has a double quote, and reads the attributes of the **Move** button. On this branch the button has only `class`, `style`, `data-qty` and `data-warehouse`, and the decoded `data-warehouse` is the full warehouse name. On `version-16-hotfix` without the fix the text after the double quote becomes an extra attribute.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427f7f719f44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.