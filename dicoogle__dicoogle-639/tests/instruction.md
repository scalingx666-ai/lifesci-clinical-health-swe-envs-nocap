# Issue

**Title:** Remove dependency on commons-codec

## Description

This removes `commons-codec` for hashing, replacing it with Guava's hashing capabilities. These changes are safe because we do not need to ensure forward compatibility with the hash output in either case.

The `commons-codec` was outdated and often resulted in conflicts at plugins depending on a more recent version.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c728ffaca8ef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.