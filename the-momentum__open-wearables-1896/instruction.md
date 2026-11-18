# Issue

**Title:** fix(frontend): backfill date range picker unreadable in dark mode

## Description

## Summary

In dark mode, the range dropdown in the "Historical backfill" section of a user's connection was hard to read. The control had a transparent background and no explicit text color, so the browser drew the native option list with a light background and light text. The dropdown now uses the theme's background and text colors, so it is readable in both light and dark mode.

## Changes

- The backfill range dropdown now uses the theme's background color instead of a transparent one.
- The dropdown text now uses the theme's text color, so both the closed control and the open option list follow the active theme.

## Effect

<img width="1202" height="1268" alt="before-after-fix" src="https://github.com/user-attachments/assets/2969f5c8-14cb-43b7-a901-c8f4bf8f7a0d" />

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Style**
  * Updated the history-range selector to use the background color token.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d18304f8076a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.