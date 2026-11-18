# Issue

**Title:** fix(manufacturing): allow closing or re-opening only a submitted Production Plan (backport #65950)

## Description

Backport of #65950 to `version-15-hotfix`. The version-16 backport is #67083.

`ProductionPlan.set_status` with **Close** or **Re-open** did not check the document status, so a call on a draft or cancelled Production Plan changed its status to Closed. Now only a submitted Production Plan can be closed or re-opened.

**Fix:** `set_status` reloads the saved document when **Close** or **Re-open** is requested and throws when it is not submitted. ()

**Changes compared with develop:** The test file conflicted on context only. The two new tests are added before `test_reserve_sub_assembly_items`. The three develop commits are one commit here. #67099 and #67101 also change `production_plan.py` and `test_production_plan.py` in other places. Each merges on its own.

 for the example and the steps to test.

### Tests

- `test_only_submitted_plan_can_be_closed_or_reopened`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_submitted_plan_can_be_closed_and_reopened`: passes on this branch, fails on `version-15-hotfix` without the fix.
- `test_production_plan.py` (complete file): 114 pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.