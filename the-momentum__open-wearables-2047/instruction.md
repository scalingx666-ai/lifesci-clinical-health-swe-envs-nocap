# Issue

**Title:** fix(backend): reject oversized direct XML uploads with 413 instead of 500

## Description

Direct Apple Health XML uploads above roughly 360 MiB returned a bare 500, because the whole file travels inside the task queue message and Redis refuses values over 512 MiB. Oversized files are now rejected up front with a clear 413 pointing to the multipart upload. .

## Changes

- Direct upload accepts files up to 200 MiB, or the product-wide `APPLE_XML_MAX_FILE_SIZE_BYTES` if that is lower. Larger files get a 413 that names the multipart endpoint to use instead. The limit sits below the queue ceiling for any content (about 288 MiB for non-UTF-8 files) and keeps the API's peak memory per upload bounded.
- A failure to queue the import now returns 503 and is logged, instead of an unhandled 500.
- The XML import worker prefetches one task per process, so it no longer holds several queued files in memory at once.
- Each XML import writes to its own temporary file. Before, two uploads with the same filename (every iPhone export is `export.xml`) shared one path, so a concurrent import could read the other user's data and save it under the wrong account.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Direct Apple Health XML uploads now enforce the applicable file-size limit, with clear guidance to use multipart uploads for larger supported files.
  * If XML processing cannot be queued, the service returns a 503 error instead of an unhandled failure.
  * Temporary files use unique names, preventing uploads with the same filename from overwriting one another.

* **Documentation**
  * Updated upload guidance and API reference to explain the 200 MiB direct-upload limit, possible lower configured limits, and oversized-file responses.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `27d68020f705`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.