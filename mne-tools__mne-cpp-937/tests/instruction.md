# Issue

**Title:** [FIX] build script return val

## Description

Fix build flag passed with --D. Should be -D.
Have build script return exit with error if build fails.

Currently our script returns success (0), regardless of the success of the build. This leads to the unfortunate circumstance of ant GH Action step running this script to pass, regardless of whether the build itself was successful. Typically this did not make itself apparent, since there are subsequent steps that would fail in the absence of a build. PR #935 had failing static builds on mac and linux, but since there are no subsequent steps, the build passed. PR #936 addresses the static flag issue.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8f2deed47a7b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.