# Issue

**Title:** agent: eval fetches data per model entry

## Description

## What

- `eval_fetch` (bool, default true) on a chat entry: whether `eval` exposes `tools.query_health_indicators`. The `local` entry sets `false`; every cloud entry keeps the default.
- `agent.eval_fetch(entry)` reads it; `_build_agent` passes an empty PTC list when it is off; `build_system_prompt` passes it to the template, whose chart rule then says "call `query_health_indicators` first; `eval` only computes on the numbers it returned".
- The key is stripped from constructor kwargs and listed in `KNOWN_ENTRY_KEYS`.

## Why

Owner's decision, 2026-10-10: cloud models keep the higher ceiling of fetching inside eval; a small local model gets one path, which is also the path MCP clients take (they have no eval) and the one the local model is being post-trained on ("B flavour").

## Verified

- Local tests (gitignored `tests/agent/test_eval_fetch.py`, 10): value parsing, the shipped config (local off, every cloud chat entry on), both prompt renderings, nothing in the request body. `CodeInterpreterMiddleware(ptc=[])` builds.
- ruff, `check_comment_style.py`, lint-imports (6 kept), shipped suite 321 passed / 13 xfailed.
- **Not yet measured:** the 24-question run with PTC on vs off. It needs the benchmark stack and runs together with the local sampling comparison; the default follows the owner's call either way.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9111aa1a3ef6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.