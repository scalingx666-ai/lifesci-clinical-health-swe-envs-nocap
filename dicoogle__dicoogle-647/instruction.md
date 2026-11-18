# Issue

**Title:** Switch to new maven repo dicoogle-public

## Description

This replaces the main Maven repository for Dicoogle and key dependencies with a new repository hosted by BMD Software.

With the dependencies not found anywhere already uploaded here, this should help new developers build Dicoogle from a fresh development environment and bring CI back to a healthy state.

TODO: provide public read access to the repository (@bastiao)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ecafbad96bb9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.