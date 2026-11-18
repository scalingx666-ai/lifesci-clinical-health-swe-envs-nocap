# Issue

**Title:** Adds logic to ignore ig-r4.json.

## Description

Adds logic to ignore ig-r4.json.
See: https://chat.fhir.org/#narrow/stream/179250-bulk-data/topic/Why.20are.20there.20two.20IG.20resources.3F/near/422507754

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1dcaaabb2702`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.