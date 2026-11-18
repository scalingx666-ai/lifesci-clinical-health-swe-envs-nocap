# Issue

**Title:** fix(server): require registered redirect URI on login

## Description

When a password or Google login request includes a `redirectUri` for a client application, `tryLogin` now requires it to match one of the client's registered redirect URIs, using the same exact match as `/oauth2/authorize`. Mismatches return `400 Invalid redirect URI`.

This replaces the warning added in #11090, now that existing clients have migrated.

Login requests without a `redirectUri` (the app's sign-in page, CLI, SDK callers) are unchanged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1a91cce07380`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.