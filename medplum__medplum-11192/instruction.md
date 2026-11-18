# Issue

**Title:** [core/MedplumClient] don't evict settled requests from the cache on abort

## Description

Components that unconditionally abort as an effect cleanup were evicting already-completed requests from the cache. Now the abort listener is removed once the request settles, and it only evicts its own entry, so aborting a superseded request no longer removes a newer one.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b314add34aef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.