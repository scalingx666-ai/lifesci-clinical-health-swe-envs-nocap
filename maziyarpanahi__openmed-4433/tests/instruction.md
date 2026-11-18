# Issue

**Title:** Run pinned d3-edge decision models on local CPU

## Description

. Depends on #4432 for verified local media.

Run `vllm-sr/d3-edge` on CPU for text, images and short videos. Loading requires an operator-allowlisted local snapshot, the verified custom-code and runtime asset digests, and the pinned offline Transformers runtime. The adapter passes in-memory pixels and video frame indices with their actual frame rate. No model weights or upstream Python files are bundled. Larger d3 checkpoints continue to use a compatible server.

Validation: `pytest -q tests/unit/structured/test_decision_d3.py tests/unit/test_decision_models_docs.py`, `make format lint format-check type-check` and mypy on both added modules. Ran `test_pinned_d3_cpu_answers_text_image_video` separately with the real revision `bee5e872f75b9c5d1405767bf244a6948b95c0af`, Transformers 5.17.0 and OS-level network denial. Synthetic image, video and text requests returned OpenMed decision results. The model is not clinically qualified by this smoke test.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b41fe524ba1a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.