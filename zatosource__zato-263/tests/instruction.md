# Issue

**Title:** GH #246 Make CID and optional param in Service.invoke_async method

## Description

Implemented it as suggested on a comment for issue #246.

@dsuch: I tested it using a couple of custom services, but I don't know for sure if some unit tests should also be included.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a7a8b4a2000c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.