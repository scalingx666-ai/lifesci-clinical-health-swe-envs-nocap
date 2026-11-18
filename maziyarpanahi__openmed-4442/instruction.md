# Issue

**Title:** Smoke-test REST, GraphQL and gRPC entry points from installed wheel and sdist

## Description

.

The installed-artifact lane in `scripts/install/smoke_check.py` now exercises every service transport, not just REST `/brief`. After the existing brief checks, the adapter profile (`[cli,service,mcp]`) builds one service runtime whose `ModelLoader` is replaced by a synthetic stand-in that only tags a synthetic marker, so no weights, tokenizer, cache or download is involved. It then runs four new checks against the installed package: `rest_pii_extract` (`POST /pii/extract` returns the expected label and offsets, and an unserved model is refused with `model_not_served` without echoing input), `graphql_query` (one `deidentify` query on `/graphql`), `grpc_stubs` (the generated `openmed.service.proto.generated` stubs are packaged files, import from the installed tree and describe `openmed.service.v1.OpenMedService`) and `grpc_loopback` (a server bound explicitly to `127.0.0.1:0` serves one `Extract` RPC that matches the REST offsets and refuses an unserved model with `INVALID_ARGUMENT`). The explicit bind means the probe works on master and after #4436 changes the default address.

Artifact mode adds a second negative control, `missing_proto_stubs`. It installs a disposable wheel or sdist copy with every generated protobuf stub removed, and it passes only when exactly `grpc_stubs` fails. Both controls now go through one table (`NEGATIVE_CONTROLS`) and a generalized `_omit_packaged_resources` helper. The helper refuses to run unless every named resource is present exactly once, so a control can't pass against an artifact that was already missing the resource. Each lane row also records the original artifact's SHA-256 digest. Rows still carry only versions, digests and fixed codes; request and response bodies, installer output and paths are never relayed. A passing lane now has eight rows (four of them controls) instead of six. The existing CI step picks this up without workflow changes. `docs/install/smoke-check.md` describes the new checks and controls.

Not covered: CI was not run for this branch. The full lane was run locally only on macOS with Python 3.11; the Linux and Windows matrix legs and the CI job timeout have not been checked with the two extra installs per artifact.

Validation: `uv build` + `python scripts/install/smoke_check.py --artifacts <dist> --constraints <uv export of cli,service,mcp> --report <file>` (8/8 rows passed, wheel and sdist, both controls rejected as expected, report contains no paths or synthetic markers, about 1m40s locally), `pytest tests/unit/install/test_smoke_check.py` (25 passed), `pytest tests/unit/test_docs_publication.py tests/unit/test_docs_language_coherence.py tests/unit/test_docs_cookbook_links.py` (passed), `ruff check .` and `ruff format --check .` (clean), `python scripts/security/check_effect_paths.py --check` (verified), `mypy` (clean), `pytest tests/ -q -m "not slow and not fuzz" --ignore=tests/unit/training/synthetic/test_dicom_overlays.py` (26171 passed, 222 skipped). The DICOM overlay test was ignored because `pydicom` is missing from the shared local venv; that failure is known on master.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cb51d6a4bc0a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.