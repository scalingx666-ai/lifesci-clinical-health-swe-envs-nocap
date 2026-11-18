# Issue

**Title:** feat(backend): log unsupported SDK record types in import summary

## Description

## What does this change?

The SDK import summary log (`apple_sdk_import_complete` and its Android/Samsung counterparts) now includes `unsupported_types`: record types this backend has no series mapping for, with a count per type.

## Why?

Records with an unknown type are skipped with a bare `continue`, so nothing says they were dropped. The case we hit: the iOS SDK adds HRV RMSSD (the-momentum/open_wearables_ios_sdk#70), mapped on the backend in #1750. An app that bumps the SDK while its Open Wearables instance is still on an older version gets a successful sync, the RMSSD samples are thrown away, and the SDK advances its anchor so they are not resent after the instance is upgraded. The only hint today is `records_saved` being lower than `incoming_records`.

I put it in the existing summary log instead of a separate warning or Sentry event. An older backend getting newer types is expected, so it should be visible, not alerting.

## How did you test this?

Ran `import_data_from_request` with this branch's code in a one-off `app` container against the local stack, for an Apple payload with 1 SDNN and 4 RMSSD records (RMSSD is not mapped on `main`):

```json
{"message": "Apple data import completed", "action": "apple_sdk_import_complete",
 "incoming_records": 5, "records_saved": 1, ...,
 "unsupported_types": {"HKQuantityTypeIdentifierHeartRateVariabilityRMSSD": 4}}
```

Not tested on a deployed instance.

## AI usage

Claude Code (Claude Opus) for tracing the import path, the change and this description.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Import completion logs now report the number of records by type that lack a supported mapping.
* **Bug Fixes**
  * Clarified import results for unmapped record types; these records remain excluded from saved data.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4de8b0833e80`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.