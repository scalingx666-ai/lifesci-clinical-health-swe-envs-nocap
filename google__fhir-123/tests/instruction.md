# Issue

**Title:** Fix race condition in the FHIR JSON parser.

## Description

Fix race condition in the FHIR JSON parser.

In the old implementation when a memo_key is found iterator on memos is accessed (read) when no mutex is held (mutex is released in the line just above). Concurrently, another thread might acquire a write lock and add a new entry to the map.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c868c92d10e7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.