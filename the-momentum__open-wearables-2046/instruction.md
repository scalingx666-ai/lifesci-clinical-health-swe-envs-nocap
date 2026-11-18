# Issue

**Title:** fix(backend): validate the user before starting an Apple XML import

## Description

A security report pointed out that an API key can import Apple Health XML data for any user. This is intended: an API key is an administrator key for the whole deployment, and per-user access goes through Mobile SDK tokens. This PR documents that and makes the XML import endpoints reject unknown or malformed user IDs before any upload starts.

## Changes

- The docs now say that an API key is an administrator key for the whole deployment, with access to every user's data, and that it must stay on the backend. The Apple XML import guide no longer describes its Bearer token as a "user login": it is the developer portal login, which has the same deployment-wide access.
- The Apple XML import endpoints accept only a UUID as the user ID. Any other value returns 422 instead of ending up in the storage object key.
- Starting an import (presigned URL, multipart upload, or direct upload) for a user that does not exist returns 404 right away. Before, an S3 upload went through and the worker skipped the file afterwards, and a direct upload was queued anyway.
- User IDs are normalized to lowercase. A multipart upload started before this change with an uppercase user ID can no longer be signed, completed, or aborted after it is deployed.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

- **Bug Fixes**
  - XML import endpoints now require UUID-formatted user IDs. Invalid IDs return a 422 response, and IDs for users who don’t exist return a 404 response. Upload URLs and import jobs aren’t created for unknown users.
- **Documentation**
  - Updated API guidance with XML import validation requirements and error responses. Clarified that API keys provide administrator-level access across a deployment and should be kept in backend code, not on user devices.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `316beb61d405`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.