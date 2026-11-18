# Issue

**Title:** Filter internal order and delivery locations by inventory usage

## Description

Internal order **Deliver From** and internal delivery **Deliver To** now list only locations whose inventory usage isn't None; an already selected location still shows.

No Jira ticket yet, so `validate-jira-ticket` will fail until a key is added to the title.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Delivery-from choices exclude the current location and locations not used for inventory. When editing an order, its existing origin remains available.
  * Delivery-to choices exclude the current location and locations not used for inventory. The selected destination remains available even if it is not used for inventory.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7386da90fc14`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.