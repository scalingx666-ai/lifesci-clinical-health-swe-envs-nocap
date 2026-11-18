# Issue

**Title:** fix(server): tighten MCP fhir-request path and SSE session handling

## Description

fhir-request now requires the resolved request path to be under the FHIR base URL.

SSE messages posted to a session are now only handled when they come from the same project membership that opened the session.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e6ea6a28f985`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.