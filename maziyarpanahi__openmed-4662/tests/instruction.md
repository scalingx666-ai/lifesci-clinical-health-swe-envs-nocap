# Issue

**Title:** compose: probe /readyz from the app service healthcheck

## Description

The `app` service now carries a healthcheck probing `http://127.0.0.1:8080/readyz` with the image's Python:

```yaml
healthcheck:
  test:
    - CMD
    - python3
    - -c
    - >-
      import urllib.request;
      urllib.request.urlopen("http://127.0.0.1:8080/readyz", timeout=3).read()
  interval: 10s
  timeout: 5s
  start_period: 15s
  retries: 6
```

Same shape as the hardened bundle's readiness probe (`deploy/openmed-compose.yaml:105-115`), on the root Compose's port 8080.

`tests/unit/service/test_docker_compose.py` gains `test_docker_compose_app_healthcheck_probes_readyz`: the healthcheck exists, its test targets `/readyz` on loopback with the bounded timeout, and the interval/timeout/start_period/retries budget is pinned.

Verification: the test module's assertion logic was run directly against the modified compose (root `conftest.py` imports the full `openmed` package, which needs the project venv — the assertions themselves all pass). Validation command from the issue: `.venv/bin/python -m pytest tests/unit/service/test_docker_compose.py -q`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b5bf9fc0c9c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.