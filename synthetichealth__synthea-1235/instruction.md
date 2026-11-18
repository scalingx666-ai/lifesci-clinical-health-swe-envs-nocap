# Issue

**Title:** RIF Bene File Splitter

## Description

Add new gradle task to split original 3 file BFD bene export into one bene file per year.

Usage: `./gradlew rifBeneSplit -Pargs="inputDir"`

Split files will be written to the same directory. The splitter will work either before or after conversion from BFD RIF to CCW RIF.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `340615e362a6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.