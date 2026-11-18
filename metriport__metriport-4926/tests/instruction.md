# Issue

**Title:** Add logic to avoid rate limiting Checkly's heartbeat monitor api

## Description

_[Release PRs:]_

Issues:

- https://linear.app/metriport/issue/ENG-1352 

### Dependencies
None

### Description
Add a DynamoDb table that will know the last time we sent a ping to checkly.
If the last ping was > 2 minutes, we will send another ping. Otherwise we will skip sending the ping.

### Testing
- Staging
  - [x] Send 2 requests to Bamboo. First should send, second should not.
  - [x] Send 2 requests to Konza. First should send, second should not. Should be separate from Bamboo.
  - [x] Make sure table exists in DynamoDb


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Heartbeat signaling for HL7 notifications with built-in 2-minute rate limiting.
  * Outbound rate limiting added across services to throttle outbound requests and protect downstream systems.
  * Outbound rate-limit resource exposed to webhook sender and API service environments.

* **Improvements**
  * Heartbeat delivery now retries on common server errors (HTTP 5xx).
  * Better error handling and logging for heartbeat/notification flows.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `759318dc7996`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.