# Issue

**Title:** fix: key result cache on model revision and generation

## Description

## Description
. Opt-in result-cache keys covered the inquiry type, text and model name only. After a promotion, pointer flip or rollback that keeps the model name but swaps the weights, the cache kept returning the previous model's results.

## Type of Change
- [x] Bug fix (non-breaking change which fixes an issue)

## Changes Made
- `make_cache_key` adds the requested model revision (`revision=` or `pipeline_kwargs["revision"]`) and a model generation counter to the hashed payload. Keys still contain no raw text.
- New `notify_model_generation_change()` (also exported from `openmed`) bumps the generation and clears the shared cache as a second guard.
- `RegistryService._commit` and `SlotRegistryService._commit` call it, so every promotion, pointer flip and rollback invalidates cached results.
- CHANGELOG entry under Fixed.

The cache is in-process, so a registry change clears the cache of the process that made it. Other replicas need to call `notify_model_generation_change()` when they switch generations. Happy to wire a cross-replica signal if you have one in mind.

## Testing
- [x] I have added tests that prove my fix is effective or that my feature works
- [x] New and existing unit tests pass locally with my changes

New tests: two revisions give different keys; a generation change misses and empties the cache; `analyze_text` reruns the pipeline after a change; promote/promote/rollback through `SlotRegistryService` each invalidate a cached entry. All check that keys contain no raw text.

`.venv/bin/python -m pytest tests/unit/core/test_result_cache.py tests/unit/core/test_registry_service.py -q`
`.venv/bin/python -m pytest tests/ -q -m "not slow and not fuzz"` → 34711 passed, 379 skipped, 4 xfailed

## Documentation
- [x] I have added docstrings to new functions/classes
- [x] I have updated the CHANGELOG.md

## Code Quality
- [x] I ran `make format`, `make lint`, and `make format-check`
- [x] I have performed a self-review of my own code
- [x] My changes generate no new warnings

## Dependencies
- [x] I have not added any new dependencies

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f83eb05b74f9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.