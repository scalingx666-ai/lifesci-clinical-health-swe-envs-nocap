# Issue

**Title:** feat: apply service security-policy reloads as validated generations

## Description

# Pull Request

## Description
Adds versioned, validated configuration generations for the REST service's
non-secret security-policy subset (request limits, authorization policy and
egress rules). A complete candidate is validated as one unit and is either
activated atomically as the next generation or rejected while the prior
generation stays active. In-flight work is pinned to one generation, so it
never mixes old and new limits or egress rules. Emergency tighten-only reloads
have explicit continuation semantics at declared checkpoints. All diagnostics
are value-free.

The module is standalone and opt-in; startup behavior is unchanged and no
existing service module is edited.

## Type of Change
- [ ] Bug fix (non-breaking change which fixes an issue)
- [x] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [x] Documentation update
- [ ] Code refactoring
- [ ] Performance improvement
- [x] Test addition/improvement

## Changes Made
- `openmed/service/policy_generations.py`: `PolicyGenerationManager`
  (bootstrap, `propose`, `activate`, `reload`, `pin`, `readiness`, `history`,
  injected clock and self-checks), immutable `SecurityPolicySettings`
  (`LimitPolicy`, `AuthorizationPolicy`, `EgressPolicy`), `PolicyPin` with
  `checkpoint()`, `PolicyGenerationMiddleware` (pure ASGI, pins each
  connection), `validate_policy_document`, `production_policy_findings`, and
  `policy_document_from_environment`.
- Every candidate field is parsed with the existing startup validators
  (`OperationalLimits`, runtime throttle parsers, `parse_max_text_length`,
  auth parsers and `parse_route_scopes`), then production posture rules for the
  `prod` profile and any injected self-check run against the assembled
  settings. Candidates must be complete; partial documents report
  `field_missing` and are never merged.
- Rejections keep the prior generation and report fixed finding codes; a
  proposed candidate that races another activation is rejected as
  `candidate_stale`; profile changes are rejected.
- Emergency reloads must be no more permissive than the active generation in
  every dimension. Pinned work observes them at `checkpoint()`, which returns
  `continue`, `rebound` (whole-generation switch to a stricter policy) or a
  sticky `halt` when neither policy is uniformly stricter. Rebinding never
  grants pinned work more than it was admitted with.
- Reports, results, history and `repr` output contain only generation numbers,
  digests, timestamps, counts, fixed codes and fixed schema field names; no
  environment values, endpoints, secrets, scope strings or route templates.
- New page `docs/security/policy-generations.md`, nav and publication entries,
  and a CHANGELOG entry.

## Testing
- [x] I have added tests that prove my fix is effective or that my feature works
- [x] New and existing unit tests pass locally with my changes
- [ ] I have tested this change with different models/inputs

Commands:

- `python -m pytest tests/unit/service/test_policy_generations.py -q`:
  61 passed (collection failed with `ModuleNotFoundError` before the module
  existed).
- `python -m pytest tests/unit/service -q`: 792 passed, 5 skipped.
- `python -m pytest tests/unit/test_doctests.py tests/unit/test_docs_publication.py tests/unit/test_public_api_docstrings.py tests/unit/test_pages_manifest.py -q`:
  138 passed, 2 skipped.
- `python scripts/security/check_effect_paths.py --check`: `effect_paths_verified`.
- `ruff check` and `ruff format --check` on the changed Python files: clean.

Coverage includes invalid and incomplete candidates (27 parametrized cases),
production posture rules, injected self-check failures, stale candidates,
pin lifetime, every emergency continuation outcome, a multi-threaded
mixed-generation test (verified to fail when pins read the active generation
instead), concurrent writers, the environment bridge with secret, endpoint and
certificate-path sentinels, and an in-process ASGI request pinned across a
reload. Documentation examples were executed locally.

## Documentation
- [x] I have updated the documentation accordingly
- [x] I have added docstrings to new functions/classes
- [x] I have updated the CHANGELOG.md

## Code Quality
- [x] I ran `make format`, `make lint`, and `make format-check` (ran the
  equivalent `ruff format` / `ruff check` commands on the changed files)
- [ ] For Swift/OpenMedKit changes, I ran `make format-swift` and `make lint-swift`
- [x] I have performed a self-review of my own code
- [x] I have commented my code, particularly in hard-to-understand areas
- [x] My changes generate no new warnings

## Dependencies
- [x] I have not added any new dependencies
- [ ] OR I have added new dependencies and they are justified because: ____

## Notes
- The production service self-check proposed in #3552 is not on `master`
  yet. Candidates are validated with the validators the service already uses
  at startup plus value-free production posture rules, and
  `PolicyGenerationManager(self_checks=[...])` accepts the #3552 check once it
  lands.
- There is no egress policy configuration on `master` beyond `OPENMED_OFFLINE`.
  The generation carries a closed egress-purpose allow-list plus a TLS
  requirement; the environment bridge derives purposes only from the presence
  of a privacy-gateway or OTLP endpoint. Wiring outbound adapters to
  `EgressPolicy.allows()` belongs to #3581.
- Out of scope: TLS and mTLS material, API-key and JWT verifier settings and
  rotation, endpoints and headers, CORS origins and trusted hosts.

## Checklist
- [x] I have read the [contributing guide](https://github.com/maziyarpanahi/openmed/blob/master/CONTRIBUTING.md), [Code of Conduct](https://github.com/maziyarpanahi/openmed/blob/master/CODE_OF_CONDUCT.md), and [maintainer guide](https://github.com/maziyarpanahi/openmed/blob/master/MAINTAINERS.md)
- [x] My commits have clear, descriptive messages
- [x] I have squashed/organized my commits appropriately

## Related Issues

Related to #3552, #3579, #3581, #3543

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `29ffa70050cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.