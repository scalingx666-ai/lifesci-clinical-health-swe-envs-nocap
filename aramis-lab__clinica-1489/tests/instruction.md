# Issue

**Title:** [FIX] Fix broken imports in CLI

## Description

This PR also proposes to add some unit tests related to the CLI client in order to avoid these kind of bugs (see issue #1485). The proposed solution consists of mocking the internal function and calling the CLI in the test with `CliRunner`. The tests then check the exit code as well as whether the mock was called and the arguments passed to it. Assuming the internal function is tested separately as well, this should be enough I believe. This testing strategy can be used for other CLI in order to close fully #1485.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `25e79021e0e0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.