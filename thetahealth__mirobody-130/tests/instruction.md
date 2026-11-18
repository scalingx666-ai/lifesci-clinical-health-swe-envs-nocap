# Issue

**Title:** agent: a thinking model reads its reasoning back

## Description

## What

`ReasoningChatOpenAI` (the client for every OpenAI-compatible entry) now re-sends each assistant step's captured `reasoning_content` on the next request, for the current turn only (`resend_reasoning`). It already captured the field; langchain-openai's request converter never sent it back.

## Why

A thinking model started every tool round of a turn from blank thinking. This is the prerequisite for thinking interleaved with tool calls, which the owner wants as every model's default (follow-up PR), and for the local model's post-training: training renders the reasoning back, so serving must too.

## Verified against the real endpoints (2026-10-10)

| Endpoint | Returns `reasoning_content` | Accepts it back |
| --- | --- | --- |
| llama.cpp b11269, MiniCPM5-2B | yes | `/apply-template` renders both steps' reasoning into `<think>`; a live two-step tool call carries it and answers |
| DeepSeek `deepseek-flash` | yes (not on every request) | 200, answer unchanged |
| DashScope `qwen3.8-flash`, thinking on | yes | 200 |
| OpenRouter `openai/gpt-6-luna` | no | 200 with the field present |
| OpenAI direct | not tested: the key in `.env` is rejected (401). It never returns the field, so nothing is re-sent | — |

Earlier turns are left out: the templates and DeepSeek drop them, and they answered another question. When the message list and the wire list do not line up one to one, nothing is sent.

Local tests (gitignored `tests/agent/test_reasoning_passback.py`, 3): current turn only, misaligned lists untouched, the real request payload carries it. ruff, `check_comment_style.py`, lint-imports (6 kept), shipped suite 321 passed / 13 xfailed.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4f0d0070933a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.