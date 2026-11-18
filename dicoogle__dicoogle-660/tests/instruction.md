# Issue

**Title:** Improve StorageInterface, add method `get`

## Description

This PR proposes a backwards-compatible extension to `StorageInterface` with default method `get`. Unlike `at`, `get` is designed to retrieve up to a single item in storage, so it does not need file system tree traversal or building up iterables and iterators.

A default implementation is provided that uses `at` underneath, but implementors may wish to override it for more efficiency.

This PR also includes a few quality-of-life improvements, including some clarifications to other methods in the plugin interface.

### Summary

- Add default method `StorageInterface#get`, to retrieve a single item from storage
   - update code in core to use it where suitable
   - also correct image servlet to only query for instances to DIM providers if specified
- Fix example code in `at`
- Clarify in `list` that a trailing forward slash means that it's a directory

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `df2dfb9afc76`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.