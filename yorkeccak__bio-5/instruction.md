# Issue

**Title:** [FIX] Default to self-hosted mode when APP_MODE not set

## Description

## Summary
- Change default behavior: apps now default to self-hosted mode
- Only switches to valyu mode when explicitly set: `NEXT_PUBLIC_APP_MODE=valyu`
- Users only need `VALYU_API_KEY` to get started - no mode config required

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8db3a67e790b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.