# Issue

**Title:** chore(server): remove the external bot function option

## Description

Remove the botCustomFunctionsEnabled config setting and support for the https://medplum.com/bot-external-function-id Bot identifier. Bots on AWS Lambda always run as medplum-bot-lambda-<bot id>. The server logs a warning at startup if the setting is still present.

Discovered by Anthropic's OSS Scanner, as vulnerability ANT-2026-VDOMIUNY

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `549291c8df71`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.