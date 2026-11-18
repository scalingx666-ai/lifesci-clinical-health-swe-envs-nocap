# Issue

**Title:** docs: add service runbooks for credential compromise, disk exhaustion and store corruption

## Description

# Pull Request

## Description

Adds service incident runbooks for four cases: a leaked API key, JWKS or job webhook secret; a compromised mTLS client certificate; a full disk under the model cache, async job store or Journey artifacts; and a damaged async job store or Journey store. Each runbook covers detection signals, containment, rotation or recovery with existing settings, verification, and what to keep out of tickets and logs. The runbooks describe current behavior only. Capabilities that have not shipped are listed as pending (#3574, #3575, #3577, #3580, #3600, #3603, #3699, #3703).

A new docs test reads the runbooks and checks every cited setting, module, import, CLI command, route, reason code, Helm value and Compose object against the repository. It includes negative controls.

## Type of Change
- [ ] Bug fix (non-breaking change which fixes an issue)
- [ ] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [x] Documentation update
- [ ] Code refactoring
- [ ] Performance improvement
- [x] Test addition/improvement

## Changes Made
- `docs/operations/runbooks/service-runbooks.md`: the overview page. It explains how settings take effect (all of them are read at `create_app`, so a restart is needed), shared rules for tickets, logs and chat, a reason-code table that points to the right runbook, and a table of pending capabilities.
- `docs/operations/runbooks/credential-compromise.md`: API keys (`OPENMED_SERVICE_AUTH_API_KEYS`; hash the new key with `hash_api_key` from a hidden prompt; verify with a curl header file so the key stays off the command line), JWKS keys (`OPENMED_SERVICE_AUTH_JWKS[_FILE]`, `kid` rules during an overlap, issuer, audience and max lifetime), and per-job webhook secrets (receiver-side overlap verifier built on `verify_request_signature`).
- `docs/operations/runbooks/client-certificate-compromise.md`: containment by removing the `OPENMED_SERVICE_MTLS_PRINCIPALS` mapping, which leaves the certificate with no scopes; denying it at the proxy; and full revocation by switching `OPENMED_SERVICE_MTLS_CA_BUNDLE` to a new CA. The service does not check CRLs or OCSP, and the page says so.
- `docs/operations/runbooks/disk-exhaustion.md`: a storage map for the Compose and Helm deployments (the Compose `openmed-cache` volume holds both models and Journey artifacts); recovery with `openmed models cache list/clear`, `openmed models verify --all` and the Journey `probe`; and the atomic write behavior of the job store.
- `docs/operations/runbooks/store-corruption.md`: the four fixed `LocalJobStore` startup messages; a check that never prints file content; quarantine and restart; recovery of the PostgreSQL Journey store, including the warning that opening the store applies pending migrations; and a backup-API copy and `integrity_check` for SQLite Journey stores.
- Navigation: a new "Service Runbooks" group after Multi-Arch Containers in `mkdocs.yml`, with matching `publication.yml` entries.
- Cross-links from `docs/security/key-management.md`, `docs/compliance/breach-notification-runbook.md` and `docs/structured/local-journey-store.md`. Pages under `docs/serving/*`, `docs/deploy/helm.md` and `docs/deploy/self-hosted-compose.md` are not edited, because open PRs change them. The runbooks link to those pages instead.
- `tests/unit/test_service_runbooks_docs.py`: checks every citation against the repository (details under Testing). It also runs the job-store check and the SQLite check snippets on synthetic stores that contain sentinels, and runs the webhook overlap verifier.
- CHANGELOG entry under Unreleased / Added.

## Testing
- [x] I have added tests that prove my fix is effective or that my feature works
- [x] New and existing unit tests pass locally with my changes
- [ ] I have tested this change with different models/inputs

Before the docs were added, the new test reported 14 failed and 3 passed. The 3 that passed were the negative and positive control tests and a store-method check. A mutation check confirmed the citation tests catch stale entries: changing one CLI flag, one env var and one reason code in a runbook made 3 tests fail.

What the test checks:
- Env vars must appear in `openmed/` or `deploy/`.
- `openmed.*` paths and `from openmed... import` names must resolve, checked by AST.
- CLI invocations must parse with the real `openmed` and `openmed.deploy.journey` argparse trees.
- `METHOD /path` citations must be in `ROUTE_POLICIES`.
- Reason codes and snake_case identifiers must appear in source.
- Helm values and Compose objects must exist in the chart and the Compose profile.
- Every `#NNNN` line must say pending.
- Code blocks must not print secrets: no `printenv`, `echo $`, `cat`, DSNs, literal auth headers or private keys.

Commands:

```bash
PYTHONPATH=$PWD .venv/bin/python -m pytest tests/unit/test_service_runbooks_docs.py -q
# 18 passed
PYTHONPATH=$PWD .venv/bin/python -m pytest tests/unit/test_doctests.py tests/unit/test_docs_publication.py tests/unit/test_public_api_docstrings.py tests/unit/test_pages_manifest.py -q
# 138 passed, 2 skipped, 32 subtests passed
PYTHONPATH=$PWD .venv/bin/python -m pytest tests/unit/test_troubleshooting_docs.py tests/unit/test_docs_ner_families_coherence.py tests/unit/test_export_matrix.py tests/unit/test_docs_language_coherence.py tests/unit/test_docs_cookbook_links.py tests/unit/test_africa_onboarding_docs.py tests/unit/test_publish_workflow_version.py tests/unit/release/test_changelog.py tests/unit/deploy tests/unit/eval/test_release_readiness.py tests/unit/processing/test_zh_segmentation_docs.py tests/unit/core/test_reference_language_packs.py -q
# 172 passed, 4 skipped, 57 subtests passed
python scripts/security/check_effect_paths.py --check
# effect_paths_verified
mkdocs build --strict
# Documentation built, no warnings
ruff check tests/unit/test_service_runbooks_docs.py && ruff format --check tests/unit/test_service_runbooks_docs.py
```

## Documentation
- [x] I have updated the documentation accordingly
- [x] I have added docstrings to new functions/classes
- [x] I have updated the CHANGELOG.md

## Code Quality
- [x] I ran `ruff format`, `ruff check`, and `ruff format --check` on the changed Python file
- [ ] For Swift/OpenMedKit changes, I ran `make format-swift` and `make lint-swift`
- [x] I have performed a self-review of my own code
- [x] I have commented my code, particularly in hard-to-understand areas
- [x] My changes generate no new warnings

## Dependencies
- [x] I have not added any new dependencies
- [ ] OR I have added new dependencies and they are justified because: ____

## Notes
- Documentation only. No service, CLI or deploy code changes.
- Behavior gaps found in current code are documented as they are, not fixed here:
  - Opening a Journey store (`probe`, `worker`, `golden`, `connect`) applies pending migrations, so there is no read-only inspection.
  - `schema_unsupported` covers both a newer schema and checksum drift.
  - API-key and JWT requests do not record the key id in access logs.
  - The job store's `webhook_delivery.error` text comes from the HTTP client.
- All examples are synthetic. Snippets read secrets from env or hidden prompts and print only fixed lines, codes and counts.

## Related Issues

Related to #3600, #3603, #3703, #3699, #3574, #3577, #3580, #3575

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `29ffa70050cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.