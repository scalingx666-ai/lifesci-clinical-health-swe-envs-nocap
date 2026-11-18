# Issue

**Title:** Adjust readme and help to remove -m.

## Description

Adjust readme and help to remove -m.

Add `=` to `--config=value` settings, even though the `=` is optional and not required.

Also, removing mentions of the `-m` feature, even though it still exists. It does more harm than good, so I don't want to advertise it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eac0b5747cb4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.