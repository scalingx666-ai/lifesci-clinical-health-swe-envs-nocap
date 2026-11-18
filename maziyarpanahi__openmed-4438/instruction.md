# Issue

**Title:** Enforce GraphQL document complexity, variable, and execution budgets

## Description

.

Adds `openmed/service/graphql_limits.py` with a versioned `GraphQLLimits` contract (document bytes, tokens, bracket nesting, syntax-tree nodes, operations, fragments, fragment cycles, variables count, compact-JSON size and depth, field depth, aliases, and selected fields as the complexity budget, plus an execution deadline), loaded from `OPENMED_SERVICE_GRAPHQL_*` environment variables with safe defaults and fail-closed parsing. `GraphQLLimitsExtension` runs ahead of `FieldScopeExtension` in `graphql_schema.py`: request budgets before parsing, a lexer scan before the recursive parser, and an iterative, cycle-safe fragment expansion before graphql-core's validation rules, so adversarial documents never reach a resolver or the model loader. `PrivacySafeGraphQLRouter` in `graphql_app.py` wraps each HTTP operation in one deadline (body decoding through result cleanup), rejects batched arrays, and maps JSON bodies nested past the decoder to the variable-depth limit. Rejections carry only the stable code (`OPENMED_GRAPHQL_LIMIT_EXCEEDED`, `OPENMED_GRAPHQL_TIMEOUT`, `OPENMED_GRAPHQL_BATCH_UNSUPPORTED`), the limit category, the configured ceiling, and the aggregate count, and are counted in the new `openmed_service_graphql_rejection_total{reason}` metric. `docs/serving/graphql.md` gains a budgets section (appended at the end of the page).

Breaking: GraphQL documents that exceed the new default ceilings (for example more than 16 aliases, field depth above 20, documents over 128 KiB, or operations running past 300 s) are now rejected; raise the matching `OPENMED_SERVICE_GRAPHQL_*` variable or send long text as a variable instead of an inline literal. Batched arrays still return HTTP 400, but with a JSON `OPENMED_GRAPHQL_BATCH_UNSUPPORTED` error instead of the plain-text body.

Model work that is already running in a worker thread when the deadline expires cannot be interrupted. It keeps its concurrency permit, in-flight count, and warm-pool lease until the worker returns, and then releases all of them, which matches the existing REST timeout contract. Both the stalled-async-resolver and stalled-worker cases are tested by advancing the loop clock, so the tests use no wall-clock thresholds.

This overlaps with open PR #3614 (GraphQL POST-only) in `graphql_app.py` and `docs/serving/graphql.md`. The changes here are additive: new router methods, one line after `include_router`, and a new section at the end of the docs page. Neither touches the lines #3614 edits.

Validation: `pytest tests/unit/service/test_graphql_limits.py` (26 passed including the Hypothesis `fuzz` property tests, 48 subtests), `pytest tests/unit/service/test_graphql_app.py tests/unit/service/test_throttle.py tests/unit/service/test_journey_resources.py tests/unit/service/test_metrics_endpoint.py` (passed), `pytest tests/ -m "not slow and not fuzz"` (26188 passed, 222 skipped; the one collection error, `tests/unit/training/synthetic/test_dicom_overlays.py`, comes from a missing local `pydicom` install and fails the same way on master), `ruff check .` and `ruff format --check .` (clean), `mypy` (clean), `scripts/security/check_effect_paths.py --check` (verified), `scripts/release/check_repo_policy.py --commits origin/master HEAD` (passed).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cb51d6a4bc0a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.