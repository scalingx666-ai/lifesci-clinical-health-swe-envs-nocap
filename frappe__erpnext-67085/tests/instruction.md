# Issue

**Title:** fix(maintenance): check that Warranty Claims and Maintenance Schedule match the Maintenance Visit company (backport #65964)

## Description

Backport of #65964 to `version-16-hotfix`.

A Maintenance Visit did not check that the Warranty Claims in its purpose rows belong to the visit's customer and company, so a visit of one company could close or reopen a Warranty Claim of another company. The visit now refuses Warranty Claims of another customer or company, and a visit for a Maintenance Schedule must also be in the schedule's company.

**Fix:** `MaintenanceVisit.validate` checks with one query that each Warranty Claim in the purpose rows has the visit's customer and company. `validate_schedule_customer` also compares the Maintenance Schedule company with the visit company. ()

**Changes compared with develop:** None. The commit applies without changes.

 for the example and the steps to test.

### Tests

- `test_visit_company_must_match_schedule`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_visit_warranty_claim_must_match_customer_and_company`: passes on this branch, fails on `version-16-hotfix` without the fix.
- `test_maintenance_visit.py` (complete file): 9 pass. 3 serial number tests (`test_visit_allows_returned_serial_delivered_before_bundles`, `test_visit_allows_returned_serial_of_the_same_customer`, `test_visit_serial_checked_against_stock_and_customer`) fail the same way on `version-16-hotfix` without this change on the local test site (`NamingSeries.get_current_value()` TypeError).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427f7f719f44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.