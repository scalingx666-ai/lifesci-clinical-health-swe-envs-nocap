# Issue

**Title:** RIF Exporter Enhancements

## Description

- Warn if simulation end date is further in the future than years of history exported
- Add a configurable cut-off date for the RIF exporter
- Rework RIF export of part D to support refills and avoid unrealistically large prescription fills

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a5c67e046ac9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.