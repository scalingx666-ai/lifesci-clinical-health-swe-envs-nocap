# Issue

**Title:** Fix DatabaseDispatcherScript Alerts to add msg ID

## Description

This  by passing the messageId from the ConnectorMessage instead of null when creating the ErrorEvent.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2f3740db44c8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.