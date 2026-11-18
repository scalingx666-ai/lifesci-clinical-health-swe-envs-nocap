# Issue

**Title:** Hide nginx version from response headers and error pages

## Description

## Proposed Changes

Pentest finding (Banner Grabbing, Low): the frontend returns `Server: nginx/<version>` on every response and nginx's default error page shows the version string on 403s, e.g. `/images/`.

- `server_tokens off` drops the version from the `Server` header and from nginx's built-in error pages

No base image or Dockerfile change. The `Server` header becomes `nginx` (no version).

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [x] Request peer reviews.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Security**
  * Server responses no longer display server version tokens. This limits the server-identifying details visible in responses. The change affects version information only; it does not alter the behavior or availability of the service. No other user-facing changes are included in this update.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `81e7515fdf4d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.