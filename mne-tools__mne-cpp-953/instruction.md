# Issue

**Title:** WIP [MAINT] enable/disable ipc/shmem when building

## Description

- Add CMake flag to build without ipc / shared memory features. (sets a macro)
- Quarantine shared memory usage in events lib.

To do:
 - [ ] Check for other uses of shared memory (mostly those related to the CMake WASM PR #938)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1e6bd6d1aa38`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.