# Issue

**Title:** Outpatient Revenue Center Updates

## Description

- Refactor bfd outpatient exporter in prep for revised revenue center mapping
- Always emit a total charge line item

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `188ce6373ef9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.