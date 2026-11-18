# Issue

**Title:** feat(backend): log SDK attribution headers in access and SDK logs

## Description

## What does this change?

The access log (`http_request`) and the SDK sync/logs batch lines now include the attribution headers the iOS SDK started sending: `sdk_version`, `sdk_platform`, `request_id`, `outbox_item_id` and `user_agent`.

A sync batch now logs:

```json
{
  "message": "Apple sync batch received",
  "action": "apple_sdk_batch_received",
  "user_id": "123e4567-e89b-12d3-a456-426614174000",
  "total_items": 4,
  ...
  "sdk_version": "0.15.0",
  "sdk_platform": "ios",
  "request_id": "6F1C2A9E-3B7D-4C55-9E0A-2D8B41F7C3A1",
  "user_agent": "OpenWearablesHealthSDK/0.15.0 (iOS 18.6.2; iPhone15,2)"
}
```

and the access log line for the same request:

```json
{
  "message": "http_request",
  "method": "POST",
  "path": "/api/v1/sdk/users/123e4567-e89b-12d3-a456-426614174000/sync",
  "status": 202,
  "request_bytes": 99,
  ...
  "sdk_version": "0.15.0",
  "sdk_platform": "ios",
  "request_id": "6F1C2A9E-3B7D-4C55-9E0A-2D8B41F7C3A1",
  "user_agent": "OpenWearablesHealthSDK/0.15.0 (iOS 18.6.2; iPhone15,2)"
}
```

In production the access log defaults to `ACCESS_LOG_LEVEL=errors`, so there these fields show up on 4xx/5xx lines only, while the SDK batch lines carry them on every accepted request.

## Why?

When SDK requests failed, our logs couldn't tell which SDK build, OS version or device sent them, and a server-side line couldn't be matched to the device-side upload log. The version only lived in the JSON body, which we can't read when the body arrives truncated. Headers are still readable in that case, and `X-Request-Id` is the same id the SDK records on its side (and reuses on a 401 retry).

All headers are optional. Older SDK versions don't send them, so the sync and logs endpoints fall back to `sdkVersion` from the body. Values come from the client, so control characters are stripped and values are capped at 256 chars.

Related issue: the-momentum/open_wearables_ios_sdk#30 (SDK side: the-momentum/open_wearables_ios_sdk#48)

## How did you test this?

I'll test it end to end on the PR branch with an SDK build that sends the new headers.

## AI usage

Claude Code (Opus 5.5) wrote the implementation and tests and drafted this description; I reviewed and edited it.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * SDK log, sync, and access records include available request details, such as SDK version, platform, request ID, and user agent.
  * When an SDK version header is unavailable, log records use the version supplied in the request body.
  * Empty values are omitted, and logged details are cleaned and limited in length.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `58dc419a4f5c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.