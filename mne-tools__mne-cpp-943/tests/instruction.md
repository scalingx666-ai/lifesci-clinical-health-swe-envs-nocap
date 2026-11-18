# Issue

**Title:** [FIX] Fix packing linux builds

## Description

Currently our deploy script sets `PackOption` to `pack` instead of `true` in the Linux section of the script. When this is later checked in the script, it causes the packing code not to run, since we check for `"pack" == "true"`. This has resulted our Linux binaries not being generated whenever a release is triggered.

This PR makes a change to the linux section of the script, where command line arguments are parsed, fixing the setting of the pack variable to `true` in case the appropriate flag is passed. This makes the functionality mirror that of the macOS section, which is behaving correctly.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `900c63b7e205`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.