# Issue

**Title:** Alohr bug fixes/better error handling

## Description

Part of ENG-1103

_[Release PRs:]_

Issues:

- https://linear.app/metriport/issue/ENG-1103

### Dependencies
None

### Description
We don't want to run the ingestion lambda in staging to not ingest potential PHI.
Save files that error'd and keep going with the rest of the files ingested.
Use Alohr's timezone instead of UTC.

### Testing
Local
- [x] Send 2 files one of which has an error in it and make sure one of them goes to webhook sender and the other into errors/filename
- [x] console log the time to make sure we are using Alohr's timezone

Staging
- [x] Deploy to staging


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Chores**
  * Short-circuits HL7 ingestion in staging for Alohr and Lahie, logging the skip to avoid processing PHI.
  * Validates Alohr configuration and propagates its timezone into runtime environments.

* **New Features**
  * Adds file name to ingest message metadata for improved traceability.
  * Exposes a configurable ingestion timezone.

* **Bug Fixes**
  * Produces timezone-aware ingestion timestamps.
  * Captures and persists per-file errors and failing message contents for easier debugging.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7104f81ced3a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.