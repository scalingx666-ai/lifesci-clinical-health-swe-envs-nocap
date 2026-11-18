# Issue

**Title:** [FIX][DOC] Modify the name of variables in the client and documentation to fit actual possibilities for `create-subjects-visits`

## Description

The variable for the input directory described with the `--help` option were incoherent with the documentation. Both the client and the documentation were inexact about it since the tool can process both BIDS and CAPS datasets.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `40b72ab8ba2d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.