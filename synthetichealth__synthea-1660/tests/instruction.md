# Issue

**Title:** Handle --help without NullPointerException

## Description

## Summary
- Treat `--help` the same as `-h` before parsing `--` arguments as config overrides
- Return after printing usage instead of calling `System.exit(0)`
- Add a regression test that verifies `--help` prints usage without an NPE or generation output

.

## Testing
- `./run_synthea --help`
- `./gradlew test --tests AppTest`

I also ran `./gradlew check`; checkstyle passed, but the full test task failed in an unrelated existing path-handling issue in `ActionsTest` because this local checkout path contains a space and the test attempted to open `Open%20Source%20projects/.../test_mapping.yaml`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c48eac705e15`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.