# Issue

**Title:** feat: declare the v3.4 reference deployment, transports and recovery objectives

## Description

# Pull Request

## Description

Declares the v3.4 reference deployment as a machine-readable contract that later gates (reference workflow, recovery drills, data-integrity evidence) can consume. The declaration lists topologies, supported transports with their security posture, replica modes, durable components with per-component recovery point and recovery time objectives, and unsupported deployments. It is validated by a JSON Schema and by an offline test that resolves every referenced REST route, worker route, MCP path, gRPC method, Python module and symbol, Compose service and volume, Helm value, manifest, and docs page in the repository. A new docs page renders the declaration row for row, and the test fails when the page and the declaration disagree.

The declaration describes current behavior: the offline Compose bundle is the reference topology; gRPC has no deployment wiring and is declared unsupported as a network transport; the async job store is a single-process local file with in-memory payloads, so its recovery objectives are `unsupported` and multi-replica async jobs are an unsupported deployment. Declared objectives are labelled `unmeasured_targets`; measuring them stays with the drill and evidence issues.

## Type of Change
- [ ] Bug fix (non-breaking change which fixes an issue)
- [x] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [x] Documentation update
- [ ] Code refactoring
- [ ] Performance improvement
- [x] Test addition/improvement

## Changes Made
- `deploy/reference/v3.4-reference-deployment.json`: the declaration. Controlled codes and repository-relative references only; no hostnames, addresses, credentials, connection strings, or patient data.
- `deploy/reference/reference-deployment.schema.json`: Draft 2020-12 schema with closed objects and enums. Each durable component must carry both `recovery_point_objective` and `recovery_time_objective`, each either `declared` (target seconds plus a basis code) or `unsupported` (reason code).
- `docs/deploy/reference-deployment.md`: renders every declaration row (topologies, services and replica modes, transports and posture, durable components with RPO/RTO, unsupported deployments) with explanatory notes and links to the existing operating procedures.
- `tests/unit/deploy/test_reference_deployment.py`: schema validation and schema negative controls; reference resolution against the live FastAPI route table, the Journey worker handler, the MCP factory default path, the committed proto, module files and top-level symbols (AST), Compose services and volumes, Helm values, manifests, and docs pages; negative controls proving each reference kind fails when missing; structural checks (unique ids, one reference topology, known services and topologies); current-behavior checks (gRPC unwired, local job store single process, loopback-only REST publish in the reference bundle); docs/declaration agreement with a drift control; and a no-hostname, no-credential, no-patient-data scan of both files with sentinel controls.
- `mkdocs.yml` and `docs/brand/system/publication.yml`: nav and publication entries next to the other deployment pages.
- `CHANGELOG.md`: Unreleased / Added entry.

## Testing
- [x] I have added tests that prove my fix is effective or that my feature works
- [x] New and existing unit tests pass locally with my changes
- [ ] I have tested this change with different models/inputs

Commands and results:

- `python -m pytest tests/unit/deploy/test_reference_deployment.py -q`: 41 passed (28 failed, 13 passed before the declaration, schema, and page existed).
- `python -m pytest tests/unit/deploy -q`: 87 passed, 4 skipped.
- `python -m pytest tests/unit/test_doctests.py tests/unit/test_docs_publication.py tests/unit/test_public_api_docstrings.py tests/unit/test_pages_manifest.py -q`: 138 passed, 2 skipped.
- `python -m pytest tests/unit/release/test_changelog.py tests/unit/test_publish_workflow_version.py tests/unit/service/test_docker_compose.py -q`: 44 passed.
- `python scripts/security/check_effect_paths.py --check`: `effect_paths_verified`.
- `mkdocs build --strict` with the docs extra: passes. On an uncommitted working tree the git revision date plugin warns that the new page has no git history; with that plugin disabled the strict build reports no warnings.
- `ruff check` and `ruff format --check` on the new test file: clean.
- Manual end-to-end control: changing one declared route to a missing path makes `test_every_referenced_route_module_and_manifest_exists` fail with `missing_route`.

## Documentation
- [x] I have updated the documentation accordingly
- [ ] I have added docstrings to new functions/classes
- [x] I have updated the CHANGELOG.md

## Code Quality
- [x] I ran `make format`, `make lint`, and `make format-check` (equivalent `ruff format` / `ruff check` on the changed Python file)
- [ ] For Swift/OpenMedKit changes, I ran `make format-swift` and `make lint-swift`
- [x] I have performed a self-review of my own code
- [x] I have commented my code, particularly in hard-to-understand areas
- [x] My changes generate no new warnings

## Dependencies
- [x] I have not added any new dependencies

`jsonschema` and `pyyaml` are already core dependencies.

## Notes
- Docs, schema, and offline tests only; no runtime code changes. The threat model and signed evidence remain with #3603, drills with #3577 and #3602.
- The declaration and schema live under `deploy/reference/` beside the manifests they describe rather than in `openmed/core/schemas/json/`, because they are a repository deployment contract and not a runtime payload shipped in the wheel.
- RPO/RTO targets (24 h / 4 h for the Journey database and artifact recovery set, re-provisioning for the model cache) follow the documented application-consistent backup and isolated-restore procedure. They are explicitly `unmeasured_targets`, not guarantees.
- Linked from the deployment docs through the mkdocs nav only; existing serving and deployment pages are left untouched to avoid conflicts with open changes.

## Related Issues

Related to #3551, #3577, #3579, #3603, #3351, #3543

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `29ffa70050cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.