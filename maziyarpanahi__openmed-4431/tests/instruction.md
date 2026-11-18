# Issue

**Title:** Add experimental local streaming speech inference with ONNX Runtime

## Description

Load a caller-supplied character-CTC model and return timed partial and final hypotheses from bounded 16 kHz PCM windows. The CPU adapter checks the graph digest, vocabulary and static signatures before runtime initialization, rejects external tensor data and never resolves a URL. Cancellation terminates active native work and fences late results. Content-free provider envelopes stay separate from protected transcripts.

. The four-file implementation is `b5d0beeaf`. It uses the existing optional ONNX dependencies and streaming protocol. The guide defines the exact log-mel frontend, expected graph layout, limits, confidence calculation and experimental status. No weights are bundled; this does not qualify a checkpoint or ship an Android package.

Validation: eight focused tests passed with network access denied, including a scalar-DFT reference comparison, fake-session cancellation and an actual ONNX Runtime CPU run on a generated synthetic graph (ONNX 1.22.0 / ORT 1.23.2). The default offline Python suite passed: 25,567 passed, 158 skipped. `make format lint format-check type-check docs-build`, explicit module mypy, API compatibility, scoped hooks, wheel/sdist and Twine, incoming attribution and secret scanning passed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `52a29d431b0e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.