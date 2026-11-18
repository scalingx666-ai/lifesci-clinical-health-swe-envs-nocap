# Issue

**Title:** llm: finish the #52 residue — Doubao off its vendor SDK, provider tables collapsed, embedding model configurable

## Description

/ #54: the residue that fix left behind, closed out under the
owner's rule that **anything naming a model or an endpoint must be overridable
from config**. Stacked on `fix-provider-base-url-override`, so this PR's base is
that branch; it retargets to `main` automatically once #54 merges.

Four commits, each independently reviewable.

### 1. Delete `get_openai_chat`

Zero callers, and it could not have had a useful one: it rejected every model
name outside a hardcoded `["gpt-4o", "gpt-4.1"]` allowlist, so asking it for a
current model raised `ValueError`. That allowlist is the anti-pattern #52 was
filed about.

### 2. Doubao through the OpenAI-compatible client; the Ark SDK is gone

The doubao/volcengine tier was the one provider built on a vendor SDK
(`volcengine-python-sdk[ark]`), declared in `[app]` and not installed in a dev
venv — so vision extraction, structured output and text completion all raised
`ModuleNotFoundError` before building a request. **The tier had never run here,
and no test could reach it.**

It never needed the SDK. Ark's `/api/v3` is an OpenAI-compatible endpoint, and
this repo's own sync volcengine client had always been a bare `OpenAI` pointed
at exactly that URL — the pyproject comment calling Ark "the one model vendor
with its own SDK rather than an OpenAI-compatible endpoint" was contradicted by
the file next to it. All three paths now go through
`client_manager.get_async_ai_client("volcengine")`, so `VOLCENGINE_BASE_URL` and
`VOLCENGINE_MODEL` reach them (Ark's Coding and Agent plans are served from
`/api/coding/v3` and `/api/plan/v3` — its URL was always a deployment question).

One behavioural difference: `thinking` moves into `extra_body`. AsyncArk took it
as a `create()` kwarg; the OpenAI SDK rejects parameters it does not declare.

What the dependency cost, measured in a clean venv on 2026-09-02: **138
`volcenginesdk*` packages, 245 MB installed** — it ships every Volcengine
product API — for one `chat/completions` call `openai` already makes.

Proof the tier is alive (this is what the handoff doc asked for): four cases
drive vision, structured output and text completion against a local
OpenAI-compatible server and assert model, `Authorization` and `thinking` inside
the body, plus a guard that nothing imports `volcenginesdkarkruntime` again. The
public gate in `test_one_key_defaults` now pins the doubao client's base_url
alongside the other three. **Not verified against real Ark** — no
`VOLCENGINE_API_KEY` on this machine.

### 3. Collapse the provider tables to what the code reads

`AIConfig` carried four kinds of unreachable literal at once:

- `_PROVIDER` / `AI_PROVIDER`, a **second** base_url table for openai,
  volcengine and dashscope with no reader anywhere — two endpoint tables is the
  precondition for the #52 class of bug;
- `_CONFIG`'s `api_path` (11 entries, no consumer), `type` (read only by a dead
  method) and `model` (nothing reads it — defaults come from the priority
  table), plus every entry no name can reach (`gpt-4o`/`gpt4o-mini`/`gpt-o3`/
  `gpt-5.2`/`doubao-lite` aliases, `gemini`, `claude`);
- openai's `api_base` was `https://api.openai.com`, missing `/v1` — harmless
  only because nothing read it;
- nine classmethods with zero callers.

What remains is the four providers `get_(async_)ai_client` builds clients for,
holding the two facts callers read. The OpenAI client is now built from
`get_provider_config` like everyone else (it read `OPENAI_API_KEY` /
`OPENAI_BASE_URL` itself — a second place deciding an endpoint), and the sync
half of `AIClientManager` goes: every sync accessor had zero callers,
`get_client`'s mapping keyed stale *model* names onto the openai client, and
`health_check` called the `get_all_providers` this commit removes.

**A real bug fell out of this**, not in the residue list: `claude` sat third in
the auto-selection order, but `async_get_text_completion`'s claude arm logged
"not supported yet" and returned `None` *without trying the next available
provider*, and `async_get_structured_output` has no claude arm at all — so an
`ANTHROPIC_API_KEY`-only deployment got silence from both helpers. It is out of
the auto-selection list; such a deployment now falls through to a provider that
answers. Agent chat is unaffected (it reaches Claude via `PROVIDERS_DEEP`).

### 4. `<PROVIDER>_EMBEDDING_MODEL`

The last table of model ids config could not reach. config.yaml recommends
self-hosting Qwen3-Embedding-8B and pointing `OPENROUTER_BASE_URL` at it — but
there was no way to say what that serving calls the model, so the request went
out as `qwen/qwen3-embedding-8b` and 404'd; the only escape was switching
provider (what the #52 E2E had to do).

`embedding_model_id()` reads the override first. Both sides already went through
that one function, so it lands on the request bodies *and* on the identity stamp
`indicator/semantic.py` checks: an override against a matrix built with the old
model raises "built by X, queries embedded by Y" instead of ranking in the wrong
vector space. `scripts/build_loinc_embeddings.py` reads the same key plus
`<PROVIDER>_BASE_URL` for the endpoint it had hardcoded — corpus and queries
have to come out of one serving. `dimensions: 1024` stays a literal on purpose:
that is the database column width, a schema fact.

### Verification

- `mirobody/` 276 passed; full local suite 1,018 passed / 3 skipped
- `lint-imports` 3 contracts KEPT; `stamp_bundle_version --check`,
  `build_runtime_index --check` OK
- `python -m build` + `check_wheel_data.py` clean; bare wheel install in a fresh
  uv venv is still **2 packages** (mirobody + numpy)
- `eval/run_eval.py --no-embed`: 7,354 cases, coverage 0.9631, wrong 0.0322
  (resolver untouched)

Not verified: real Ark and real Anthropic traffic (no keys here), and the
browser E2E was not re-run this round.

Left deliberately open: merging the two provider-configuration systems
(`utils/config/llm.py` vs `utils/llm/config.py`). `docs/roadmap.md` asks for
per-provider characterisation tests first; this PR only updates the counts that
entry cites.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `38dbe2009873`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.