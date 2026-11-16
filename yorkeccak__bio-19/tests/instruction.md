# Issue

**Title:** Simplify Bio social preview

## Description

## Summary
- remove banners, navigation, avatars, badges, links, logos, and footer clutter from the social card
- retain only the current Bio research interface and three core workflow cards
- use a versioned image URL to bypass stale social-preview caches

## Verification
- `pnpm build`
- verified the image is an RGB PNG at 1200 x 630
- scanned staged changes for secrets

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5fcb49500519`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.