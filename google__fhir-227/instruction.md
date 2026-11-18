# Issue

**Title:** Upgrade protoc-gen-go Version

## Description

Upgrade protoc-gen-go Version

- Don't skip the `go install` for `protoc-gen-go` if it's already installed. The
  `go install` command is still needed to upgrade the `protoc-gen-go` version if
  it's already installed but at an older version.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2eb0d913794c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.