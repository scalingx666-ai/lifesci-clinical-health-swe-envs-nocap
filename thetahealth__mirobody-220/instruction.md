# Issue

**Title:** fix(bench): read the chat stream without stalling on a large event

## Description

## What was wrong

`benchmarks/local_models/run.py` read the chat SSE stream with `iter_lines(decode_unicode=True, chunk_size=1)`. `requests` rebuilds the unfinished line on every read, so assembling one line costs time in the square of its length. With a model that reads photos itself, a `read_file` result carries the photo as base64 (up to 1.5 MB in one event). That line took minutes to arrive. The question's deadline is checked once per line, so it never fired, and the recorded `seconds` measured the reader instead of the answer.

## What changed

- `_sse_lines` reads with urllib3's `read1`, which returns whatever has arrived, and splits the lines itself. Each event is still timed when it arrives, whether the stream is chunked or not.
- Why not `iter_lines(chunk_size=None)`: it waits for the end of a stream that is not chunked. The existing `test_real_sse_delivers_thinking_before_server_finishes` failed on it.
- The `chunk_size == 1` assertion in the mocked stream test is replaced by a `raw.read1` mock.
- New `test_real_sse_large_event_arrives_before_the_deadline` sends a 300 KB event from a real local server, once closed by the connection and once chunked.

## How it was checked

| Reader | 100 KB event | 200 KB | 1.5 MB |
| --- | --- | --- | --- |
| main (`chunk_size=1`) | 2.7 s | 10.2 s | not arrived after 150 s (deadline 30 s) |
| this PR | 0.02 s | 0.01 s | 0.02 s |

Measured against a uvicorn `StreamingResponse`. Per-event timings (`first_tool_s`, `first_text_s`) are identical on a paced stream.

- The new test fails against main's reader in 10 s, both framings: `AssertionError: the runner was still reading one 300 KB event after 10 s`. Before the test ran the read in a thread, it hung past 280 s.
- Gates:
  - `ruff check mirobody examples benchmarks/local_models`: clean
  - `compileall`: clean
  - `lint-imports`: 6 kept, 0 broken
  - library-layer import: fine
  - `pytest -q`: 1252 passed, 121 skipped, 12 xfailed

## Follow-up: a broken stream fails its question, not the run

- The new reader reads `Response.raw` itself, past requests, which had raised urllib3's errors as its own. `ask()` catches `RequestException`, and the question loop has no other guard.
- So a connection dropped mid-event, or a read timeout, escaped as `urllib3.exceptions.ProtocolError` / `ReadTimeoutError` and ended the whole run. On main, both were recorded as that question's error.
- `_read_arrived` now raises them the way requests' `iter_content` does.
- New `test_real_sse_broken_stream_is_a_recorded_case_failure` covers two cases: a chunked stream dropped mid-event, and one quiet past a 1 s read timeout. Both failed with the urllib3 errors before 508f3804; both now record the error and keep the event that arrived before the break.
- `pytest -q`: 1254 passed, 121 skipped, 12 xfailed. The six real-socket stream tests passed in each of five repeated runs.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c54a81f47e79`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.