# Issue

**Title:** OBLS-996 Unmark the receipt bulk-pass regression spec as pending

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:** https://openboxes.atlassian.net/browse/OBLS-996

**Description:**

Fixes the red `Regression Tests` runs on `feature/obaf-integration` since #6249.

The regression suite marked `ReceiptBulkPassUnitSpec` "a failing shipment does not stop the next one from being received" as `@PendingFeature`, with the defect #6249 fixed as its reason: the catch block in `ReceiptService.receiveInboundShipments` logged `${requisitionId}`, a name not in scope, so the `MissingPropertyException` escaped the catch and one failing shipment stopped the whole bulk pass. With #6249 merged the feature passes, and Spock fails a pending feature that passes ("Feature is marked with @PendingFeature but passes unexpectedly"). #6249's own checks predate the suite on this branch, so it did not show up there.

This removes the marker (and its import), making the feature a normal test that guards the fix; also asserts that the second shipment's backorders are queued and the failed one's are not, so the test shows the pass really continued. It also updates the comment in `AutoReceiptIntegrationSpec` that still called the defect pending. Test code only.

**Verification:**

- `regressionTest --tests ReceiptBulkPassUnitSpec`: 2 tests, 0 failures.
- With the old `${requisitionId}` log line put back in `ReceiptService`, the feature fails, so it catches the defect if it returns.

### :camera: Screenshots & Recordings (optional)

N/A, test code only.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `43c381fc304a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.