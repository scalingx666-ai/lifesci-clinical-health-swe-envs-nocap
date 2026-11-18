# Issue

**Title:** docs: deprecate Open Wearables native health scores

## Description

## What does this change?

Adds a deprecation notice for the OW native Sleep Score and Resilience Score, which are removed from this repo on November 6, 2026 and will be distributed as a separate package, available as an extension under a different license. See [Health Scores](https://docs.openwearables.io/scores/health-scores#deprecation-of-ow-native-scores).

## Why?

The `/health-scores` endpoint stays and keeps returning OW scores computed before November 6, but no new ones are created after that date, so integrations relying on them would quietly stop getting fresh records. The notice shows how to check that up front: OW scores are the ones with `provider: internal`, and `?provider=internal` returns exactly them. The endpoint is not marked `deprecated` in OpenAPI because it isn't going anywhere.

## How did you test this?

Ran the docs locally with `mint dev` and checked the warning and the new section on the Health Scores, Sleep Score and Resilience Score pages, the updated roadmap card, and the endpoint description in the API reference.

## AI usage

Claude Code (Claude Opus) for finding where in the docs and code the notice belongs.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Documentation**
  * Clarified that native Sleep and Resilience scores are scheduled to stop being computed and leave the repository on November 6, 2026. They will be available separately as an extension under a different license.
  * Documented that the health-scores endpoint will remain available and continue returning previously computed Open Wearables scores after that date.
  * Updated guidance on identifying internal-provider score records and clarified that Recovery and Activity scores remain.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bec35eec3314`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.