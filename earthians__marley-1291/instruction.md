# Issue

**Title:** fix: make Approve All and Reject All work after a panel component is rejected

## Description

Issue description
When every component in a panel is approved, the parent panel is marked Approved. Rejecting one component creates a new draft copy, but the parent still says Approved. Approve All then skips the new copy, while Reject All tries to cancel that draft and fails.

Steps to reproduce issue before this change:-
1. Create a diagnostic report with a panel that has at least two components.
2. Enter a result for each component and click Approve All. Confirm they are all approved.
3. Reject one component. A draft replacement is created.
4. Click Approve All again. 
Expected: the replacement is approved.                                                                                                                                                          Actual: it is skipped.
5. Repeat steps 1–3 with a fresh report, then click Reject All. Expected: the components still approved are rejected, and the draft replacement remains editable. Actual: the action fails while trying to cancel the draft.


Changes made:-

1)observation.py
- Updated Approve All to look inside an approved panel and approve any new draft component.
- Updated the approval eligibility check so the consumables preview includes that component.
- Updated Reject All to reject components that are still approved while leaving draft replacements editable.


2)test_diagnostic_report.py
- Added a test for Approve All after rejecting a component in a fully approved panel.
- Added a test for Reject All in the same situation, checking that the draft replacement remains untouched.

Note:- Extension of PR #1287 . Needs backport after merging PR #1288

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f7120aefedff`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.