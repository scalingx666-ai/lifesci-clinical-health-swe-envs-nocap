# Issue

**Title:** Default gRPC to loopback and add explicit TLS and mTLS server credentials

## Description

.

The gRPC service now defaults to `127.0.0.1:50051` and checks its listener before it creates or binds a server. The new `openmed/service/grpc_security.py` loads the server certificate chain, private key and optional client CA with `cryptography`. It checks that the PEM parses, that the key matches the leaf certificate, and that the leaf is inside its validity window, then builds grpcio `ssl_server_credentials` (mutual TLS when a client CA is set). Plaintext on wildcard, routable or named hosts is refused unless `allow_insecure_remote_dev=True` is passed under the `dev` or `test` profile. Under any other profile, including `prod` and an unset `OPENMED_PROFILE`, setting that override fails with `grpc_insecure_dev_override_rejected`. `serve()` raises `GrpcStartupError` on any refusal, and also when grpcio raises or reports port 0, so it never returns a server that is not listening. The error carries a stable reason code, a controlled category and, at most, a certificate SHA-256 fingerprint. It never carries paths, addresses, PEM text or key bytes, and the exception context is suppressed. `create_grpc_server()` now accepts `interceptors` so the per-RPC auth work in #3547 can plug in, and `GrpcListener.report()` gives a value-free summary for the security-profile self-check. `docs/serving/grpc.md` documents the transport policy, the reason codes and restart-based certificate rotation, and `docs/serving/mtls.md` links to it. #4190 (gRPC health) also edits `create_grpc_server()` and `serve()`, so whichever lands second needs a small merge there.

Breaking: `DEFAULT_GRPC_ADDRESS` changes from `[::]:50051` to `127.0.0.1:50051`, and `serve()` on a non-loopback address now needs `tls=GrpcTLSConfig(...)`. To migrate, pass server TLS files, or for a disposable lab set `allow_insecure_remote_dev=True` with `OPENMED_PROFILE=dev`.

Not covered: certificate issuance, production trust roots and a deployed Compose or Helm gRPC listener. gRPC has no CLI or container entrypoint yet. TLS and mTLS were tested only with ephemeral synthetic certificates on loopback.

Validation: `pytest tests/unit/service/test_grpc_tls.py` (85 passed), `pytest tests/unit/service/test_grpc_server.py tests/unit/service/test_mtls_auth.py` (15 passed, includes the protobuf stub drift check), `ruff check .` and `ruff format --check .` (clean), `python scripts/security/check_effect_paths.py --check` (effect_paths_verified), `mypy` (clean), `pytest tests/ -m "not slow and not fuzz"` (26250 passed, 222 skipped, 11332 subtests passed; 1 collection error in `tests/unit/training/synthetic/test_dicom_overlays.py` because `pydicom` is not installed in the local venv, which fails the same way on master).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cb51d6a4bc0a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.