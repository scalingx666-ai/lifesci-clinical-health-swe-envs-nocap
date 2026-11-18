# Issue

**Title:** enh: add uv venv dev setup option

## Description

## Summary

Adds [uv](https://docs.astral.sh/uv/) as an alternative to conda for the development environment. Conda stays the main documented path.

- `Makefile`: new `make venv` target. It creates `.venv` with Python 3.12 (the same version as `make dev-setup`) and runs `uv pip install -e ".[dev]"`. One `PYTHON_VERSION` variable now sets the version for both targets.
- `CONTRIBUTING.md` and `doc/development/contributing.rst`: a short note, "Alternative without conda", with `make venv` and the two plain uv commands.
- `AGENTS.md`: agents can use conda **or** uv.

The `.*` rule in `.gitignore` already ignores `.venv`. This PR adds no `uv.lock`: a library must work with a range of dependency versions, and a lock file pins only one set.

This is the first step of the performance work in #576. The later benchmarks use this environment.

## AI use

AI was used. Model: Claude Opus 5.5 (Claude Code). It wrote the Makefile target, the documentation text and this description. A human (the author) set the scope; human review is pending.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Mr7sVWVWnqWZUEYkYUaeLy

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b493c41add47`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.