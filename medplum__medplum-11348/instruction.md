# Issue

**Title:** fix(deps): upgrade zod to v4 and override dompurify to 3.4.17

## Description

The MCP SDK (1.32.2) now accepts zod ^3.25 || ^4.0, so the v3 hold in upgrade.sh is no longer needed. Under zod 4 the SDK treats z.any() as required, so fhir-request's body is now explicitly optional (GET requests with no body were rejected).

monaco-editor pins dompurify 3.4.15 exactly; override to 3.4.17.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1de5b813022d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.