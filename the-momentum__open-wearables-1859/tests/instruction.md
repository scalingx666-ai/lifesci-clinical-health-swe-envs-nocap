# Issue

**Title:** feat(backend): report SDK payload S3 offload in telemetry

## Description

## What does this change?

Adds `sdk_payload_s3_offload` to the `features` block of the [telemetry](https://docs.openwearables.io/dev-guides/telemetry) ping, and documents it.

## Why?

[SDK payload offload](https://docs.openwearables.io/dev-guides/raw-payload-storage#sdk-payload-offload) is the main fix for Redis running out of memory during large SDK backfills, but we can't see which instances use it. `raw_payload_storage` doesn't tell us either, because offload works with archiving turned off. We suspect few people know the option exists, since it's only described on the raw payload storage page, and this will show whether that's true.

Kept `schema_version` at 1 since the change only adds a field.

## How did you test this?

Built the payload in a one-off app container with `SDK_PAYLOAD_S3_OFFLOAD` set to `false` and then to `true`. In each case, the `features` block reported the value that was set:

```json
"raw_payload_storage": "s3",
"sdk_payload_s3_offload": true,
```

I didn't check that the field arrives at the telemetry endpoint.

## AI usage

Claude Code (Opus 5.5) for the change and the PR text.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Telemetry now reports whether SDK sync payloads are routed through S3 rather than Redis.
* **Documentation**
  * Updated the telemetry guide to describe this feature flag and show it in a sample payload.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bcb37d7cdf83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.