# Issue

**Title:** llm: honor <PROVIDER>_BASE_URL everywhere, add <PROVIDER>_MODEL

## Description

.

## What was broken

`OPENROUTER_BASE_URL` redirected embeddings (`Config.get_llm`) but the vision and structured-extraction clients were built from `AIConfig`'s hardcoded table — an upload's OCR still called `openrouter.ai` and failed against self-hosted gateways. The file saved, no indicators appeared, exactly as reported. Reproduced against a recording local gateway: before the fix the configured endpoint received **zero** requests while the extraction returned empty.

## The fix

One rule at one choke point, no merging of the two config families:

- `AIConfig.get_provider_config` overlays `<PROVIDER>_BASE_URL` onto the table's `api_base` — openrouter (vision + structured) and volcengine inherit it immediately.
- The missing `dashscope` table entry is added (its absence is why that URL was pasted at three call sites; `health_check()` also couldn't see the provider). The cached dashscope clients and `_get_qwen_client` now build from the table.
- The bare OpenAI constructor passes `base_url` explicitly: the SDK only reads the **env var**, so a YAML-only `OPENAI_BASE_URL` was silently ignored.
- `get_async_openrouter_client` is replaced by a generic `get_async_ai_client(provider)`; the dead `base_url` field in the qwen vision entry is deleted.
- **New: `<PROVIDER>_MODEL`** picks the chat/structured model per provider, mirroring the existing `<PROVIDER>_VISION_MODEL` — without it a redirect is half-usable, because openrouter's default model id 404s on most self-hosted endpoints.
- `config.yaml` documents the mechanism with a DashScope example; CHANGELOG updated.

## Evidence

- New public gate `test_base_url_override_reaches_the_file_extraction_clients` pins all four construction paths to the override **and** to the official-gateway fallback when unset (sibling of the existing `get_llm` pin).
- Local behaviour suite (fake OpenAI-compatible gateway, gitignored `tests/`): `unified_file_extract` and `async_get_structured_output` traffic actually arrives at the configured endpoint with the configured model and auth header.
- Full battery green: 276 passed (`mirobody/`), `lint-imports` 3 contracts kept, bundle/index `--check` OK.
- End-to-end on the local stack with `OPENROUTER_BASE_URL=https://dashscope.aliyuncs.com/compatible-mode/v1`, `OPENROUTER_VISION_MODEL=qwen3-vl-flash`, `OPENROUTER_MODEL=qwen-flash`, and a DashScope key as `OPENROUTER_API_KEY` (a key that openrouter.ai would 401): real report photo upload → vision OCR → structured extraction → **19 indicators** written and shown in the UI with the report's true date, zero provider fallbacks; agent chat answered from the data via `query_health_indicators`.

Note for reviewers: pointing provider A's base_url at provider B's *official* endpoint additionally requires B to tolerate A's request dialect (e.g. OpenRouter's `reasoning` extra_body — DashScope tolerates it; gateways like LiteLLM/one-api do too). That caveat is documented next to the config keys.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `27ec868244e7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.