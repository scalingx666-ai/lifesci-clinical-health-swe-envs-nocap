# Issue

**Title:** Match preview to current Bio landing page

## Description

## Summary
- replace the social card with a version derived from the current live Bio landing page
- preserve the new workflow-led interface, navigation rail, controls, workflow cards, source strip, and DNA background
- use a versioned asset URL to bypass stale social-preview caches

## Verification
- `pnpm build`
- verified the image is an RGB PNG at 1200 x 630
- scanned staged changes for secrets

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `001c5b54a876`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.