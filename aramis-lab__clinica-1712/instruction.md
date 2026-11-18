# Issue

**Title:** [FIX] PET-Volume : Add `build_petpvc_name` as a task

## Description

## Description
When using option `--pvc_psf_tsv` with an actual file, code crashes because of improper  Nipype formatting (input name, type). This option is currently not tested in the CI.


## Key Changes Made
- Added the function `build_pet_pvc_name` from pet surface utils in the tasks with type checking compatible with Nipype
- Fixed input format for one node

## Checklist
- [x] Coding style respected (eg: '_' at the beginning of variable names, private or public functions, docstrings, ...)
- [ ] Unit tests added and passing
- [x] Functional testing completed (on Linux and macOS)
- [x] Instantiation tests passing

## How to Test
<!-- Steps to reproduce or validate -->
- Run the pet-volume pipeline with the option `--pvc_psf_tsv`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d2753f7a6527`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.