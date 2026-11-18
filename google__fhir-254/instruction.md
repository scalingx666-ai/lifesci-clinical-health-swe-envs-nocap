# Issue

**Title:** Now that ProtoGeneratorV2 is used for generating core R4 protos, adds a regression test to prevent introducing unintended changes.

## Description

Now that ProtoGeneratorV2 is used for generating core R4 protos, adds a regression test to prevent introducing unintended changes.

Fully qualifies some field types, so that the generated descriptor protos match the compiled ones.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c74e22ce2cba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.