# Issue

**Title:** Explicitly handle the Reference.uri field in JSON (de-)serialization for FHIR protos since the json name caused a conflict that is no longer permitted in all languages.

## Description

Explicitly handle the Reference.uri field in JSON (de-)serialization for FHIR protos since the json name caused a conflict that is no longer permitted in all languages.

This commit has no visible change in behavior, it is a pre-factor for removing the conflicting field name from the generated protocol buffers.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `669c086756f2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.