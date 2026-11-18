# Issue

**Title:** fix(server): return a uniform error when the $ai provider request cannot be sent

## Description

When the outbound request to the AI provider fails before a response is received, `$ai` now reports a single fixed message instead of forwarding the underlying error.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `54295a43473d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.