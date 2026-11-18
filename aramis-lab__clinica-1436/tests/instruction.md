# Issue

**Title:** [TEST] Refactor and test function `print_images_to_process`

## Description

The function `print_images_to_process`:

https://github.com/aramis-lab/clinica/blob/d505ac2f23119856844fef9b285cf47e774ceb94/clinica/utils/ux.py#L11-L35

is used in various pipelines but was not tested in isolation.
This PR proposes:

- to add these unit tests
- simpler implementation relying on the builtin `defaultdict` instead of `get_unique_subjects`
- to give more possibilities for customization (logging level and maximum number of lines)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `57cbde74d6b2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.