# Issue

**Title:** Cherry Pick for 8476 Allow NOPs for unchanged resources with auto-versioned reference…

## Description

8476 Allow NOPs for unchanged resources with auto-versioned references (#8486)

(cherry picked from commit f539d52709c2d7a5f31a3f641245b4417246f87a)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7b47cea2c6ca`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.