# Issue

**Title:** agent: every chat model thinks between tool calls

## Description

**Stacked on #130** (the reasoning passback). Merge #130 first; this PR's diff then shrinks to its own commit.

## What

- `AGENT_THINKING: medium` in `config.llm.yaml`: the thinking level every chat model gets between its tool calls. An entry's new `thinking_level` overrides it (`off` is allowed). Passed through `build_llm_clients(thinking=…)`; utility surfaces are untouched.
- Two dialects that were missing:
  - **openrouter** (detected from the host): `extra_body.reasoning.effort`; the `reasoning` field OpenRouter returns is captured like `reasoning_content`.
  - **chat_template** (llama.cpp / vLLM): `extra_body.chat_template_kwargs.enable_thinking`. The `local` entry declares `thinking_style: chat_template`.
- `thinking_level` is stripped from constructor kwargs (it was reaching `model_kwargs`, i.e. the request body).
- `docs/model-choice(.zh-CN).md`: a table of what each entry does, as measured.

## Measured (2026-10-10, one two-step lookup, real endpoints)

| Entry | Before | After |
| --- | --- | --- |
| `local` MiniCPM5-2B | thinks both steps | identical output (temperature 0): the template already thought |
| `deepseek` | thinks | thinks |
| `qwen` | thinks | thinks, budget 8192 |
| `gpt` (OpenRouter) | no visible thinking | thinking visible after the tool result (386 chars) |
| `claude-sonnet` (OpenRouter) | none | none: routed to Google Vertex, 0 reasoning tokens even at `effort: high` |
| `openai` direct | none | none: `reasoning_effort: none` is what lets GPT-6 Sol call a tool on Chat Completions; key in `.env` returns 401 |
| `gemini-flash`, `claude` direct | thoughts not returned | **not verified**: the Gemini API refused this machine's region, and there is no Anthropic key. Both now get `medium` through their existing dialects (`include_thoughts` + budget; adaptive thinking). Please verify before merging |

Local tests (gitignored `tests/agent/test_thinking_default.py`, 8): dialect detection, entry `extra_body` kept, `off`, field capture, table default vs entry level, the shipped config, nothing in the body. ruff, `check_comment_style.py`, shipped suite 321 passed / 13 xfailed.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9111aa1a3ef6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.