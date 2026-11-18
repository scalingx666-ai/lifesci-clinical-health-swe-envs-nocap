# Issue

**Title:** Check roles before loading plugins and warn about missing roles

## Description

Summary:

- Add user role loading to the beginning of the program, so that plugins are aware of the roles which are effectively registered.
- When loading web UI plugins, send a warning if the given role does not exist and ignore it from the plugin descriptor during that run.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5507ee7d8b8b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.