# Issue

**Title:** Apply the request deadline to the PII extraction stream and bound slow consumers

## Description

.

`ServiceRuntime.stream_pii_extract` (`openmed/service/runtime.py`) now runs every `append` and `finish` window as a worker future under one request deadline. The deadline is checked before a window starts and bounds each wait through a shielded `wait_for`. When it passes, `StreamDeadlineExceeded` becomes the existing value-free `timeout` NDJSON error line on `/pii/extract/stream`. If the stream stops while a window is still running (deadline or disconnect), the window's done-callback releases the model reference, and the window is handed to the request's `RequestWork`. That keeps the permit and drain slot held, counted as orphaned work, until the worker returns, the same way the single-shot REST timeout path works.

Both NDJSON routes now go through `NDJSONStreamControls` and `BoundedNDJSONResponse` in `openmed/service/streaming.py`, which add:
- a max-event cap that ends with `stream_event_limit`;
- a write-idle bound enforced by `StreamWriteIdleMiddleware` at the outermost ASGI send. It abandons the blocked write, offers one `stream_write_idle` line for a short grace period, then leaves the response incomplete so the server closes the connection;
- an explicit close of the body generator;
- a new `RequestWork.hold()` in `throttle.py`, so a stream keeps its concurrency permit and drain token until the body ends. Today they are released as soon as headers are sent.

Overlap with #4137 (#3901): this PR does not touch `_iterate_deidentify_ndjson`. Once #4137 lands, its deferred de-identification window should be passed to `NDJSONStreamControls.retain`, so the permit follows the model reference the same way it does for the extraction stream.

Breaking:
- `/pii/extract/stream` now ends at the profile `timeout`. Raise the profile timeout for very long extraction streams.
- Both streams stop after a write has been blocked for 30 s, or after 100,000 lines. Tune `OPENMED_SERVICE_STREAM_WRITE_IDLE_SECONDS` and `OPENMED_SERVICE_STREAM_MAX_EVENTS`; both must be positive and cannot be disabled.
- Streams hold their `OPENMED_SERVICE_RATE_LIMIT_MAX_CONCURRENCY` permit for the whole body. Raise that limit if long streams should run alongside single-shot calls.
- Extraction-stream model errors now end with a value-free `bad_request` or `internal_error` line instead of an aborted response.

Validation:
- `python -m pytest tests/unit/service/test_stream_bounds.py tests/unit/service/test_streaming_deidentify_endpoint.py -q`: 32 passed. The new module uses synthetic classifiers, a loop-clock jump for the deadline, and a raw ASGI consumer that stops reading. 25 of its 27 tests fail on master: the deadline test hangs until the worker returns, and the disconnect test sees the model reference drop to 0 while the worker is still running.
- The issue's reproduction (`timeout=0.1` with a streamer that needs 3.5 s) now returns in 0.10 s with exactly one `timeout` line. Master took 3.53 s and returned only `final`.
- Manual run against uvicorn 0.41 (h11) with a raw socket client that stops reading and a 0.5 s idle bound: the producer stopped after 16 of 5000 events, the model reference and drain slot went back to baseline, and uvicorn closed the connection without a chunked terminator.
- `python -m pytest tests/ -q -m "not slow and not fuzz" --ignore=tests/unit/training/synthetic/test_dicom_overlays.py`: 27077 passed, 226 skipped. `test_dicom_overlays.py` is ignored because `pydicom` is not installed locally; this is the same on master.
- `python -m pytest tests/unit -k "docs or publication or mkdocs or postman or openapi or troubleshooting"`: 195 passed, 14 skipped. The strict MkDocs build is left to CI.
- `ruff check .` and `ruff format --check .`: clean.
- `python scripts/security/check_effect_paths.py --check`: `effect_paths_verified`, after classifying the two new ASGI send wrappers as operational.
- `mypy`: no issues.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7655442ff060`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.