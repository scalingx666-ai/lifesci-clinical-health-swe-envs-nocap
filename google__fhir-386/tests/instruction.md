# Issue

**Title:** Change all references of std::string_view to absl::string_view

## Description

Change all references of std::string_view to absl::string_view

absl:string_view is recommended over std::string_view and avoid emscripten compliation error on string conversion (web assembly).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2e6c10f7c43b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.