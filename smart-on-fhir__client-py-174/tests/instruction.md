# Issue

**Title:** Implement Pagination Features for FHIRClient and Bundle Classes

## Description

### Overview
This pull request aims to address pagination functionalities as outlined in issue #172. The implementation includes the following key changes:

- Refactoring `FHIRSearch` perform() and perform_resources with iterations.
- Adding `__iter__` method to the `Bundle` class to handle pagination.
- Moving pagination logic to `_utils.py` for better modularity and reuse.
- Adjusted tests to accommodate the new iterable-based approach.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e19a87133de3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.