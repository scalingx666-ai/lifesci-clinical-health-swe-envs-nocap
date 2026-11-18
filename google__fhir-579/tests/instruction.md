# Issue

**Title:** Accept `name` in `fhir_proto_library` alongside deprecated `proto_library_prefix` and rename `proto_library_prefix` to `name` across `BUILD` call sites.

## Description

Accept `name` in `fhir_proto_library` alongside deprecated `proto_library_prefix` and rename `proto_library_prefix` to `name` across `BUILD` call sites.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d131ab2e8d48`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.