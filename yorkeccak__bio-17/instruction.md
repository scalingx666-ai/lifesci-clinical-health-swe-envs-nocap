# Issue

**Title:** Refresh Bio social preview

## Description

## Summary
- replace the full-page screenshot with a dedicated 1200 x 630 social preview
- improve legibility in Slack, X, LinkedIn, and other link cards
- point Open Graph and Twitter metadata at the new Bio-specific asset

## Verification
- `pnpm build`
- verified the image is an RGB PNG at 1200 x 630
- scanned the staged changes for secrets

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b39d1c34409b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.