# Issue

**Title:** care-circle: a malformed member id is a denial

## Description

`resolve_subject()` ran `int()` on the requested member id. That id comes from a URL parameter or a request body, and every caller except the upload path catches only `CareCircleDenied`, so a non-integer `target_user_id` answered **500** instead of **403**.

It now raises `CareCircleDenied("not a member id")`. A blank id still means the caller's own record. The routers already map `CareCircleDenied` to their refusal response, so no caller changes.

**Verified**
- New test over `abc`, `1 OR 1=1`, `2.5`, `0x10`, `--` (denied) and blank/space (own record): 5 failed before the fix, all pass after.
- Full local suite with and without the fix: identical failure set apart from those 5 (the remainder are 1.5.1-only tests on this `main`-based branch).
- `pytest mirobody` 69 passed · ruff clean · comment style 0 problems · lint-imports 6 kept.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3e9173a1668e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.