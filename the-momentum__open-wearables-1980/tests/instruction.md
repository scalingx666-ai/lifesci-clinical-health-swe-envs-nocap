# Issue

**Title:** feat(backend): log SDK app state and sync trigger

## Description

## What does this change?

Two more SDK headers are read into the same log fields as the existing attribution headers (#1811):

| Header | Log field | Values |
|---|---|---|
| `X-Open-Wearables-App-State` | `app_state` | `foreground`, `background` |
| `X-Open-Wearables-Sync-Trigger` | `sync_trigger` | `healthkit_observer`, `bg_app_refresh`, `bg_processing`, `start`, `restore`, `resume`, `reset`, `foreground`, `unlock`, `network` |

They show up on `http_request` and `apple_sdk_batch_received`, so syncs can be counted by `app_state` and `sync_trigger` in whatever log backend a deployment uses.

The SDK integration guide gets a short section listing every header the iOS SDK sends and the log field it ends up in. The existing ones weren't documented either.

## Why?

We can't currently tell whether a live sync ran in the background. The SDK already reports `taskType` in `device_state`, but only through `/logs`, and it only calls `/logs` during the historical export. Users who are past that export send nothing there, so their app state isn't recorded anywhere. Checking whether background sync works after an SDK release meant guessing from the gaps between sync timestamps.

I didn't make `/logs` send `device_state` on live syncs, because that's one more request per sync. A header costs nothing and lands on the line we already query.

`app_state` is deliberately not named `task_type`. `/logs` already logs `task_type` from the body and merges both dicts into one `log_structured` call, so a header with the same name would raise on duplicate kwargs.

Values come from the client and go through the same sanitising as the other headers: control characters are stripped and values are capped at 256 chars. Older SDKs don't send these headers, so the fields are just missing.

SDK side: the-momentum/open_wearables_ios_sdk#75

## How did you test this?

- `tests/utils_tests/test_sdk_request_metadata.py`, `tests/api/v1/test_sdk_sync_logging.py` (new case: both fields on `apple_sdk_batch_received`), `test_access_log.py` and `test_sdk_logs.py`: 48 passed, run in the backend container.
- End to end: the Flutter example app built against the SDK branch (release build, iPhone 13, iOS 27.0.1), syncing to a local stack with this change. A batch sent after reopening the app:

  ```json
  {
    "message": "Apple sync batch received",
    "action": "apple_sdk_batch_received",
    "total_items": 641,
    "sdk_version": "0.16.0",
    "sdk_platform": "ios",
    "app_state": "foreground",
    "sync_trigger": "foreground",
    "user_agent": "OpenWearablesHealthSDK/0.16.0 (iOS 27.0.1; iPhone14,5)"
  }
  ```

  The first export came in as `foreground` / `start`, matching the `device_state.taskType: foreground` that the SDK sent to `/logs` at the same moment.

  After the app had been killed, iOS relaunched it in the background for a HealthKit delivery:

  ```
  POST /sync  401  app_state=background  sync_trigger=healthkit_observer
  (token refresh)
  POST /sync  202  app_state=background  sync_trigger=healthkit_observer   6 items
  POST /sync  202  app_state=background  sync_trigger=healthkit_observer  27 items
  ```

  The 401 replay carries the same values as the attempt it repeats.

Not tested: Android. The Android SDK doesn't send these headers yet.

## AI usage

Claude Code (Opus) for the investigation (server logs and stored SDK payloads), the code, the tests and the first draft of this description.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Server logs can now include the app’s foreground or background state and the event that triggered an SDK sync. Requests without these optional headers continue to be accepted.
* **Documentation**
  * SDK integration docs describe the optional sync headers, their log fields, and supported minimum SDK versions.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8adbd0ae519d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.