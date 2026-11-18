# Issue

**Title:** fix(backend): reject oversized direct XML uploads before spooling to disk

## Description

The direct XML upload endpoint checked the file size only after the whole request had been parsed and written to a temporary file, and before the API key check. An oversized upload, even one without a valid API key, could fill the API container's disk before it got a 413. Stacked on #2047.

## Changes

- A request that declares a body larger than the direct upload limit is rejected with 413 before any of the body is read. Clients that wait for `100 Continue`, like curl, don't upload the body at all.
- A request without a declared size is cut off with 413 as soon as the received bytes exceed the limit plus a small margin for the multipart framing, so nothing beyond that reaches the disk.
- ~~In these early rejections the exact file size isn't known yet, so the 413 detail says "File is over N MiB" instead of giving the size.~~ _(Changed during review by Sebastian Kalisz:)_ The 413 detail no longer gives the file size (#2047), so the early rejections use the same message as the endpoint's own check.
- An oversized request now gets 413 even when its API key is missing or invalid, because the size check runs first.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Oversized direct XML uploads are rejected with a clear message reflecting the applicable upload limit.
  * Requests that exceed the limit are stopped before the full upload is processed, whether the size is declared upfront or the request arrives in chunks.
  * Rejected uploads are not parsed or queued for processing.
  * Multipart formatting overhead is accounted for when enforcing the direct-upload size limit.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8e73b52532a0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.