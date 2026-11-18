# Issue

**Title:** Improve warning message for duplicated Resource Bindings

## Description

It's more useful when both sources of the duplication are described in the logs. The current log line only has the obfuscated method signature and doesn't help pin down the source.

As the existing test asserts, bindings are in a `FILO` (or rather `LIFO`) order, where only the most recent binding will be returned on lookup, so the log message is correct regarding the replacement.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3e114d86937b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.