# Issue

**Title:** agent: the local model declares its input window

## Description

## What

- `config.llm.yaml`: the `local` entry declares `profile.max_input_tokens: 24000`. llama.cpp serves it at `c = 32768`; 24000 + `max_tokens` 6144 fits.
- `agent/harness.py`: a model that declares a window pages a tool result out to the virtual filesystem past a quarter of that window (`tool_offload_limit`), never above deepagents' default. The replacement `FilesystemMiddleware` carries the read-only mount permissions.

## Why

- Undeclared, deepagents compacts at a fixed 170000 tokens, which a 32k model never reaches: long turns overflowed first (two of the 24 questions ended in `ContextOverflowError`).
- deepagents counts 4 characters per token. MiniCPM5's tokenizer on the tool tables of `benchmarks/local_models`: 1.85 characters per token (Chinese-heavy), 2.21 (English). Its default 20000 let up to ~45000 real tokens sit inline.

## Verified

- The real `local` client built from `config.llm.yaml`: `profile.max_input_tokens` 24000, summarization trigger `('fraction', 0.85)`, offload limit 2700 (deepagents units, about 6000 real tokens).
- Local tests (gitignored `tests/agent/test_local_context.py`, 7): threshold arithmetic, no change for cloud windows, permissions kept, deepagents replaces a same-named middleware in place, `assemble` hands it over, the entry fits the served `c`.
- ruff, `check_comment_style.py`, lint-imports (6 kept), shipped suite 321 passed / 13 xfailed.

CHANGELOG lines for this and the following PRs come in one small PR at the end, so the PRs do not conflict on the Unreleased header.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4f0d0070933a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.