# Issue

**Title:** [REF] PET-Surface : Replace `fslmerge` with a python function

## Description

## Description
For the PET Surface pipeline the external software FSL is required, but is only used to perform a "merge" of nifti images. The same can be achieved with a nibable function and avoids having to download a whole external library just for this basic application.

## Key Changes Made
- New merge function introduced for PET Surface
- Unit test added
- Documentation modified

## Checklist
- [x] Coding style respected (eg: '_' at the beginning of variable names, private or public functions, docstrings, ...)
- [x] Unit tests added and passing
- [x] Functional testing completed (on Linux and macOS)
- [x] Instantiation tests passing
- [x] Non-regression tests passing (on Linux and macOS)
- [x] CI database updated (if required) - not required
- [x] Documentation updated (if required)


## How to Test
Run the PET Surface pipeline without the FSL dependency.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6fb94fb54697`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.