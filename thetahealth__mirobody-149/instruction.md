# Issue

**Title:** agent: eval-only as_of pins the agent's clock per request

## Description

## What
Frozen eval runs replay old data and ask about it dated after it (e.g. data ending 2026-09-01, question asked on 2026-10-14 about "the last 30 days"). The agent read the real system clock everywhere, so these runs found nothing and answered "cannot tell".

`POST /api/chat` now accepts an optional `as_of` field: an ISO date (`"2025-10-18"`, read as noon that day in the request's timezone) or an ISO datetime (`"2025-10-18T07:30:00"`, used as given; a naive one takes the request's timezone).

## How it's gated
Honoured only when the server has `EVAL_AS_OF_ENABLED` set (off by default, read the same way as the repo's other boolean flags). A request carrying `as_of` while the setting is off is refused explicitly (`-5`), not silently ignored. A bad format is refused with `-2` even when the setting is on.

## How it's carried
`mirobody/agent/clock.py` is one small module: a `ContextVar` holding the pinned moment, `now(tz)` (the pin if set, else the real clock), `as_of(moment)` (a context manager scoping the pin to one turn), `parse_as_of`, and `eval_as_of_enabled`. `chat/turn.py::run` sets it before entering `_pump`, so the turn's spawned background task (`asyncio.create_task` copies the ambient context) sees it too, and concurrent requests never see each other's moment, since each already runs in its own task/context.

Every agent read of "what time is it" now goes through it: `prompt.turn_note`, `prompt.build_system_prompt`'s `current_time`, `hitl.parse_date_answer`'s default `today`, and `RecordTool._clock()` (the tools' own clock hook, used by both `query_health_indicators` and `query_medications` for their default windows). The existing `_now` test-injection on tools is unchanged and still wins when set. Stored wall-clock facts (`th_messages.created_at`, a file's `upload_time`, etc.) are untouched; only the agent's own "now" moves.

## Verified
- New regression tests: `tests/agent/test_eval_clock.py` (9 cases) — `turn_note` shows the pinned date; two concurrent "turns" with different `as_of` each see only their own, including through a spawned background task; a tool's `_clock()` reads the pin when no `_now` is injected, and `_now` injection still wins; the API refuses `as_of` when the setting is off (`-5`), accepts it when on, and refuses a bad format (`-2`) even when on.
- `pytest -q tests/agent/test_eval_clock.py tests/agent`: 450 passed, 22 failed — the 22 failures are pre-existing and identical (same names) on `origin/main` with the same gitignored `tests/` tree (API drift in the local-only test fixtures, unrelated to this change; confirmed by running the exact same command against a clean `origin/main` worktree).
- `pytest -q mirobody tests -k "chat or agent or prompt or tool"`: failure set is byte-for-byte identical to the same command on `origin/main` (34 failures, diffed to zero).
- `uvx ruff check mirobody`: clean. `lint-imports`: all 6 contracts kept. `scripts/check_comment_style.py mirobody`: 0 problems.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f4fcee681b3a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.