# Issue

**Title:** fix(maintenance): check that Warranty Claims and Maintenance Schedule match the Maintenance Visit company (backport #65964)

## Description

Backport of #65964 to `version-15-hotfix`. The version-16 backport is #67085.

A Maintenance Visit did not check that the Warranty Claims in its purpose rows belong to the visit's customer and company, so a visit of one company could close or reopen a Warranty Claim of another company. The visit now refuses Warranty Claims of another customer or company, and a visit for a Maintenance Schedule must also be in the schedule's company.

**Fix:** `MaintenanceVisit.validate` checks with one query that each Warranty Claim in the purpose rows has the visit's customer and company. `validate_schedule_customer` also compares the Maintenance Schedule company with the visit company. ()

**Changes compared with develop:** None. The commit applies without changes.

 for the example and the steps to test.

### Tests

- `test_visit_company_must_match_schedule`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_visit_warranty_claim_must_match_customer_and_company`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_maintenance_visit.py` (complete file): 12 pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.