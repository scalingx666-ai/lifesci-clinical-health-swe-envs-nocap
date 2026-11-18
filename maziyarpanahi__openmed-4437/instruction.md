# Issue

**Title:** Bind authenticated principals to Journey purpose, consent, and export policy

## Description

.

Journey reads now take their authority from the authenticated principal instead of request parameters. The new transport-neutral `openmed/service/journey_access.py` adds a `JourneyAccessContextProvider` protocol, a `ConfiguredJourneyAccessContextProvider` that resolves role, attributes, namespaces, purposes, export postures and consent from operator grants (`OPENMED_SERVICE_JOURNEY_GRANTS` or `OPENMED_SERVICE_JOURNEY_GRANTS_FILE`, keyed by credential type plus exact subject, with optional opt-in signed-JWT claims and a consent hook), and a single `JourneyAccessGate` that both REST (`app.py`) and GraphQL (`graphql_schema.py` / `graphql_app.py`) call. Request parameters may only narrow the context. Widening returns a typed denied page with a stable code (`role_not_granted`, `namespace_not_granted`, `attribute_not_granted`, ...). Missing, expired, unavailable, unknown-consent or withdrawn-consent context denies. Anonymous Journey reads are refused outside the `dev` and `test` profiles. Each decision is appended to a bounded, value-free audit log with a keyed principal digest (`auth.principal_digest`), the decision ID, the request digest and the policy and grant versions. `JourneyResourceCatalog.deny` / `JourneyAccessPolicy.deny` give denial pages one shared shape.

Breaking: `GET /v1/journey/resources` and GraphQL `journeyResources` no longer trust the `role`, `attributes`, `namespace`, `purpose`, `consent_state` or `export_policy` arguments. Their defaults are now null, meaning "use the grant". Anonymous reads under the default `prod` profile return `anonymous_access_denied`, and authenticated principals without a grant return `access_context_missing`. Migration: define a grant per principal in `OPENMED_SERVICE_JOURNEY_GRANTS`, or pass `create_app(journey_access_context_provider=...)`. The OpenAPI and GraphQL SDL snapshots are regenerated.

Not covered: there is no gRPC Journey projection today. The gate accepts a `grpc` transport so a future handler can reuse it. The first-party Python, TypeScript and Go clients still send the legacy default access parameters, so callers whose grant excludes `clinician`, `care_review`, `default` or `metadata_only` must pass explicit selections until the clients omit them. The audit log is in-memory with an optional sink, and the digest key is random per process unless an embedder supplies one; durable audit custody is left to the deployment.

Validation: `pytest tests/unit/service/test_journey_principal_policy.py` (52 passed: API-key, JWT, mTLS, missing-context, downgrade, expiry, withdrawal, anonymous-prod and REST/GraphQL parity cases), `pytest tests/ -m "not slow and not fuzz"` (26217 passed, 222 skipped; the only error is a collection-time `ModuleNotFoundError: pydicom` in the untouched `tests/unit/training/synthetic/test_dicom_overlays.py`, caused by the local venv lacking `pydicom`), `ruff check .` and `ruff format --check .` (clean), `scripts/security/check_effect_paths.py --check` (verified), `mypy` (clean).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cb51d6a4bc0a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.