# Issue

**Title:** Replace builtin casts with proto-specific casts for protobuf types.

## Description

Replace builtin casts with proto-specific casts for protobuf types.

There is a protobuf experiment to "devirtualize" messages, allowing protobuf to manage the dynamic dispatch of messages. When enabled, it breaks builtin dynamic/down casts, so the protobuf-specific alternatives should be preferred.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d0ef5e6353bf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.