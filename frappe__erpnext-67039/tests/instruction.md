# Issue

**Title:** fix(controllers): check Item read permission in item_manufacturer_query (backport #65939)

## Description

Backport of #65939 to `version-16-hotfix`.

`item_manufacturer_query` is the search behind the **Manufacturer** field in the items table of purchase transactions. It returned the manufacturers and manufacturer part numbers of any item, without a permission check. Now the user must be able to read the Item.

**Fix:** return no rows when `item_code` is missing or is not a string, and check read permission on the Item before the Item Manufacturer rows are read. ()

Follow-up test commit: covers a missing, empty and non-string `item_code`. ()

**Changes compared with develop:** The function signature conflicted, because develop added type annotations to it in an earlier change. The signature of this branch is kept and only the change in the body is applied. The test file conflicted only because develop has other tests next to the new test. Only the new test is added. This PR and the other backports to `version-16-hotfix` that change `queries.py` and `test_queries.py` (#67040, #67041) change different functions and different places in the test file. Each PR merges on its own. The follow-up test commit is not in #65939.

 for the example and the steps to test.

### Tests

- `test_item_manufacturer_query_requires_item_read_permission`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_item_manufacturer_query_needs_a_single_item_code` (follow-up commit): with no `item_code`, `None`, an empty string or a list, a Purchase User and a Website Manager get no rows and no error. It fails when the `item_code` check is removed.
- `test_queries.py` (complete file): all tests pass except `test_item_query_with_percent_in_permitted_company`, which fails with an SQL syntax error in `item_query`. It fails the same way on `version-16-hotfix` without this change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427f7f719f44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.