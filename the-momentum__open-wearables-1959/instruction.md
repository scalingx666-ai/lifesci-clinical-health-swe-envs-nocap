# Issue

**Title:** chore(backend): remove unused async database session

## Description

## What does this change?

Removes the async engine, `AsyncSessionLocal` and `AsyncDbSession` from `app/database.py`. Nothing in the backend used them.

## Why?

SQLAlchemy 2.1 no longer installs `greenlet` by default, and importing `sqlalchemy.ext.asyncio` without it raises an `ImportError`. Because `app/database.py` imported it at module level, the app, the test suite and the OpenAPI export all fail to start on the Dependabot bump in #1920. The other fix is `sqlalchemy[asyncio]`, but that keeps a dependency around for code we don't use. If we move to async sessions later, we can add both back.

Unblocks #1920.

## How did you test this?

Ran `from app.main import api` with `sqlalchemy==2.1.4` and `greenlet` blocked (`sys.modules['greenlet'] = None`):

```
main:   ImportError: The SQLAlchemy asyncio module requires that the Python 'greenlet' library is installed. ...
branch: app.main OK
```

I also grepped `app/`, `tests/`, `scripts/` and `mcp/`, and nothing references the removed names. I didn't bump SQLAlchemy here, so #1920 will still hit the `ty` errors from the new typing.

## AI usage

Claude Code (Claude Opus 5.5) - traced the CI failure in #1920 to the missing greenlet and made the change.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Refactor**
  * Backend database access now uses synchronous sessions. Asynchronous database session support has been removed; this change does not introduce a new user-facing feature.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `602aafc5fadd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.