# Issue

**Title:** chore(server): log caller identity on authentication errors

## Description

Authentication errors were logged without any caller identity, and anything logged while authenticating had no request or trace ID. That made it impossible to tell which login or membership was behind a failed request, such as a rejected X-Medplum-On-Behalf-Of header.

Authenticate within an unauthenticated request context so auth-time logs carry the request and trace IDs, and log the login, project, membership, profile, and on-behalf-of header when a request fails after the caller is known.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `33721124c9d7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.