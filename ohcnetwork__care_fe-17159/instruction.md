# Issue

**Title:** Show External Supply only at Store locations

## Description

Hides the External Supply nav group and blocks `/inventory/external/*` pages unless the current location's inventory usage is Store.

No Jira ticket yet, so `validate-jira-ticket` will fail until the title has a key.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * External supply purchase orders and deliveries are now shown only for locations with Store inventory.
  * External inventory pages display a translated unavailable message for locations without Store inventory, with a loading indicator while location details load.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ce83ae1582aa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.