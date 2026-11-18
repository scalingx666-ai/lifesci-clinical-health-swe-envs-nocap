# Issue

**Title:** feat: reload API-key and JWT verifier generations atomically

## Description

# Pull Request

## Description
Adds caller-controlled verifier generations for REST API-key and JWT authentication. Each generation is a complete set of API-key hashes, JWKS and JWT issuer/audience/lifetime bounds. It is validated as a whole, published as one immutable snapshot, and retired through a bounded overlap window or immediate revocation. Every authentication decision runs against exactly one generation and is pinned to its ID, serial, snapshot epoch and role. A rejected reload keeps the last valid generation active. Receipts, metrics, status and errors carry only fixed codes, counts, labels, timestamps and digests.

The new module reuses `authenticate_api_key`, `authenticate_jwt` and the existing API-key/JWKS/audience parsers from `openmed/service/auth.py`. It does not reimplement JWT checks, and `auth.py` and `app.py` are unchanged.

## Type of Change
- [ ] Bug fix (non-breaking change which fixes an issue)
- [x] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [x] Documentation update
- [ ] Code refactoring
- [ ] Performance improvement
- [x] Test addition/improvement

## Changes Made
- `openmed/service/auth_generations.py` (new):
  - `VerifierGenerationSpec` and `parse_verifier_generation` read the input.
  - `validate_verifier_generation` checks completeness and freezes the contents.
  - `VerifierGenerationRegistry` provides `stage`, `activate`, `reload`, `revoke`, `view`, `status` and `metrics`.
  - `GenerationDecision`/`GenerationPin` record which generation admitted a request, and `GenerationReceipt` records each lifecycle call.
  - `GenerationalServiceAuth` is a `ServiceAuth` subclass that apps install with `app.state.auth = GenerationalServiceAuth.replacing(app.state.auth, registry=...)`.
- Validation rejects:
  - incomplete generations (no verifiers, or JWKS without an issuer and audience);
  - malformed hashes and JWKs;
  - unsupported key types and algorithms, and private JWK members;
  - weak keys (HS256 secrets under 32 bytes, RSA moduli under 2048 bits by default);
  - duplicate key IDs, hashes and kids;
  - out-of-range leeway and lifetime.
- Lifecycle rules:
  - serials must increase on every activation, and generation IDs cannot be reused;
  - overlap is bounded by `max_overlap_seconds`, and at most one previous generation is accepted, until `retire_at` (exclusive);
  - a credential carried over during an overlap must be identical (`api_key_conflict` / `jwk_kid_conflict`);
  - the number of staged generations is capped;
  - revocation takes effect immediately and fails closed.
- Concurrency: lifecycle calls are serialized under a lock and publish a new snapshot with one reference assignment. Readers take one snapshot per decision, and inputs are deep-copied so later caller mutation has no effect.
- Clock: the injected clock is read once per decision and used for both overlap boundaries and JWT time claims. Invalid readings fail closed.
- Docs page `docs/security/auth-verifier-generations.md`, plus entries in `mkdocs.yml`, `docs/brand/system/publication.yml` and `CHANGELOG.md`.

## Testing
- [x] I have added tests that prove my fix is effective or that my feature works
- [x] New and existing unit tests pass locally with my changes
- [x] I have tested this change with different models/inputs

`tests/unit/service/test_auth_verifier_generations.py` uses synthetic keys and an injected clock. It covers:
- overlap admission, and rejection at and after the boundary (API key, HS256, RS256);
- zero-overlap cutover, and staging without activation;
- the one-previous-generation overlap bound, and out-of-range overlaps;
- revocation, including fail-closed revocation of the active generation;
- stale serials and ID reuse;
- 23 malformed or incomplete generation cases, each checked to leave the active snapshot unchanged;
- cross-generation conflicts, including a recheck at activation;
- document parsing through the existing parsers;
- caller mutation after reload;
- a pinned view across a reload;
- invalid clocks;
- a six-reader threaded reload test that fails on any partial set, unpinned decision or future key;
- sentinel leak checks over receipts, status, metrics, reprs and errors;
- deterministic receipt digests;
- middleware rotation without a restart (`@pytest.mark.integration`).

As a negative control, I patched the registry to publish a half-populated generation before the full one, and the concurrency test caught it.

Commands (from the repo root, with `PYTHONPATH=$PWD`):
- `python -m pytest tests/unit/service/test_auth_verifier_generations.py -q`: 43 passed (it failed at collection with `ModuleNotFoundError` before the module existed)
- `python -m pytest tests/unit/test_doctests.py tests/unit/test_docs_publication.py tests/unit/test_public_api_docstrings.py tests/unit/test_pages_manifest.py tests/unit/service/test_auth_verifier_generations.py -q`: 181 passed, 2 skipped, 32 subtests passed
- `python -m pytest tests/unit/service -q`: 774 passed, 5 skipped, 258 subtests passed
- `python scripts/security/check_effect_paths.py --check`: `effect_paths_verified`
- `ruff check` and `ruff format --check` on changed Python files: clean

## Documentation
- [x] I have updated the documentation accordingly
- [x] I have added docstrings to new functions/classes
- [x] I have updated the CHANGELOG.md

## Code Quality
- [x] I ran `ruff format`, `ruff check`, and `ruff format --check` on the changed files
- [ ] For Swift/OpenMedKit changes, I ran `make format-swift` and `make lint-swift`
- [x] I have performed a self-review of my own code
- [x] I have commented my code, particularly in hard-to-understand areas
- [x] My changes generate no new warnings

## Dependencies
- [x] I have not added any new dependencies
- [ ] OR I have added new dependencies and they are justified because: ____

## Notes
- Scope: this covers the verifier lifecycle only. TLS/mTLS reload, token issuance and identity-provider discovery are out of scope. mTLS principals pass through unchanged and carry no generation pin.
- Wiring: the registry is caller-controlled. Nothing reads files or the environment to trigger reloads, and the default app keeps the static `OPENMED_SERVICE_AUTH_*` verifiers. To opt in, set `app.state.auth`, which the existing middleware already reads on every request, so `app.py` needs no change.
- Metrics: counters are exposed through `registry.metrics()` as code-keyed integers. They are not yet exported through the Prometheus registry.
- Stricter defaults: a generation with JWKS always enforces an issuer, an audience and a finite maximum token lifetime, which is stricter than the non-production static defaults.

## Checklist
- [x] I have read the [contributing guide](https://github.com/maziyarpanahi/openmed/blob/master/CONTRIBUTING.md), [Code of Conduct](https://github.com/maziyarpanahi/openmed/blob/master/CODE_OF_CONDUCT.md), and [maintainer guide](https://github.com/maziyarpanahi/openmed/blob/master/MAINTAINERS.md)
- [x] My commits have clear, descriptive messages
- [x] I have squashed/organized my commits appropriately

## Related Issues

Related to #807, #3580, #3543

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `29ffa70050cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.