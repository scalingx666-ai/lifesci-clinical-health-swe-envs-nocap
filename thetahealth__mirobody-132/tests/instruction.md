# Issue

**Title:** agent: the prompt says where the models run

## Description

## What

- `agent/prompt.py`: `deployment_facts(chat_alias)` reads the routes in effect (the chat entry, `resolve_route("ocr")` or `("vision")`, `resolve_route("text")`) and states each model and where it runs. `place()` says *on this machine* (loopback, `host.docker.internal`, the compose `llama` services), *on your own network* (private addresses, dotless and `.local` hosts), or *sent over the internet to <host>*; an entry with no `base_url` uses its family's API host.
- `mirobody.jinja`: a "Where the models run" section when there are facts, telling the model to answer "which model are you / is my data uploaded / where do my questions go" from them.

## Why

A model asked those questions answered from its own beliefs. The document routes are the part a slogan gets wrong: on this machine's real config (`.env` with an OpenRouter key), choosing `local` for chat renders

> In this deployment, the answering model minicpm5-2b (on this machine); report photos and scanned pages are read by google/gemini-3.8-flash (sent over the internet to openrouter.ai); text extraction, titles and summaries use google/gemini-3.8-flash (sent over the internet to openrouter.ai).

Only when every route is local or on the person's network does it add "None of these is a cloud service."

## Verified

- Rendered against the real `config.yaml` + `config.llm.yaml` + `.env` for `local`, `deepseek`, `gemini-flash` (a chat-only family `resolve_named` cannot serve; read from the entry), `claude-sonnet`.
- Local tests (gitignored `tests/agent/test_deployment_facts.py`, 16): every place class including `[::1]`, LAN, dotless, `.local`, an unset endpoint name; all-local, mixed, nothing configured; the section renders only with facts. `test_prompt_render.py` still passes.
- ruff, `check_comment_style.py`, lint-imports (6 kept), shipped suite 321 passed / 13 xfailed.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9111aa1a3ef6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.